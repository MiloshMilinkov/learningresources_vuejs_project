<template>
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
                <BaseButton type="submit" >ADD RESOURCE</BaseButton>
            </div>
        </form>
    </BaseCard>
</template>

<script>
export default {
    data() {
        return {
            titleInput: '',
            descriptionInput: '',
            linkInput: ''
        }
    },
    methods: {
        SubmitResourceData(){
            this.addResource(this.titleInput, this.descriptionInput, this.linkInput);
        }
    },
    inject:['addResource']
}
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