<template>
    <ul id="myUL">
        <li>
            <input type="checkbox" v-model="checkFlag" @change="changeFlag()"/>
            <div v-if="!editFlag">
                <span>{{ propsData }}</span>
                <br>
                <button class="Edit" @click="editChnageFlag()">Edit</button>
                <button class="close" @click="$emit('removeClick', propsData);">Delete</button>
            </div>
            <div v-else>
                <span>Edit Name for "{{ propsData }}"</span>
                <input type="input" :value="propsData" @change="changeEdit($event)"/>
                <br>
                <button class="edit_cancle" @click="editChnageFlag()">Cancel</button>
                <button class="edit_save" @click="eEditSave(propsData)">Save</button>
            </div>
        </li>
    </ul>
</template>

<script>
export default {
    props: {'propsData' : String},
    data() {
        return {
            checkFlag: false,
            editFlag: false,
            editText: '',
        }
    },
    created: function(){
        console.log('Create');
    },
    methods: {
        changeFlag() {
            this.$emit('checkFlag', this.checkFlag);
        },
        editChnageFlag() {
            this.editFlag = !this.editFlag
        },
        changeEdit(e) {
            this.editText = (e.target).value;
        },
        eEditSave(type) {
            //if(/^\W/g.test(this.editText) || this.editText === '') {
                this.$emit('editSave', type, this.editText);
                this.editFlag = false;
            //}
        }
    }
}
</script>

<style scoped>

</style>