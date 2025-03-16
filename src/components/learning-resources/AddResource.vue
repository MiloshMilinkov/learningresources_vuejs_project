<template>
    <BaseDialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
        <template #section>
            <p>Unfortunately, at least one input value is invalid.</p>
            <p>Please check all inputs again.</p>
        </template>
        <template #actions>
            <BaseButton @click="confirmError">Okay</BaseButton>
        </template>
    </BaseDialog>
    <BaseCard>
        <form action="" @submit.prevent="SubmitResourceData">
            <div class="form-control">
                <label for="title">TITLE</label>
                <input id="title" name="title" type="text"  v-model="titleInput">
            </div>
            <div class="form-control">
                <label for="description">DESCRIPTION</label>
                <textarea id="description" name="description" rows="3" v-model="descriptionInput"></textarea>
            </div>
            <div class="form-control">
                <label for="link">LINK</label>
                <input id="link" name="link" type="url" v-model="linkInput">
            </div>
            <div>
                <BaseButton type="submit">{{ isEditing ? 'UPDATE RESOURCE' : 'ADD RESOURCE' }}</BaseButton>
            </div>
        </form>
    </BaseCard>
</template>

<script>
export default {
    props: ['editingResource'],
    data() {
        return {
            titleInput: '',
            descriptionInput: '',
            linkInput: '',
            inputIsInvalid: false,
            resourceId: null
        };
    },
    watch: {
        editingResource: {
            immediate: true,
            handler(newResource) {
                if (newResource) {
                    this.titleInput = newResource.title;
                    this.descriptionInput = newResource.description;
                    this.linkInput = newResource.link;
                    this.resourceId = newResource.id;
                } else {
                    this.titleInput = '';
                    this.descriptionInput = '';
                    this.linkInput = '';
                    this.resourceId = null;
                }
            }
        }
    },
    computed: {
        isEditing() {
            return !!this.resourceId;
        }
    },
    methods: {
        SubmitResourceData() {
            if (this.titleInput.trim() === '' || this.descriptionInput.trim() === '' || this.linkInput.trim() === '') {
                this.inputIsInvalid = true;
                return;
            }
            this.addResource(this.titleInput, this.descriptionInput, this.linkInput, this.resourceId);
        },
        confirmError() {
            this.inputIsInvalid = false;
        }
    },
    inject: ['addResource']
};
</script>

<style scoped>
label{
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}
input,
textarea{
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}
input:focus,
textarea:focus{
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}
.form-control{
    margin: 1rem 0;
}
</style>