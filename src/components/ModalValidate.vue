<template>
    <modal
            title="Modal with form"
            @close="$emit('close')"
    >
        <!-- body -->
        <div slot="body">
            <form @submit.prevent="">
                <div class="form-item" :class="{ errorInput: $v.name.$error }">
                    <label>Name:</label>
                    <p class="errorText" v-if="!$v.name.required">Field is required!</p>
                    <p class="errorText" v-if="!$v.name.minLength">Name must have at least {{
                        $v.name.$params.minLength.min }} !</p>
                    <input
                            v-model="name"
                            :class="{ error: $v.name.$error }"
                            @change="$v.name.$touch()"
                    >
                </div>
                <label>Email:</label>
                <input v-bind="email">
                <button class="btn btnPrimary">Submit</button>
            </form>

        </div>
    </modal>

</template>

<script>
    import {required, minLength, email} from 'vuelidate/lib/validators'

    import modal from '@/components/UI/Modal.vue'

    export default {
        components: {modal},
        data() {
            return {
                name: '',
                email: ''
            }
        },
        validations: {
            name: {
                required,
                minLength: minLength(4)
            },
            email: {
                required,
                email
            }
        }

    }
</script>

<style lang="scss">
    .form-item .errorText {
        display: none;
        margin-bottom: 8px;
        font-size: 13.4px;
        color: #de4040;
    }
    .form-item {
        &.errorInput .errorText{
            display: block;
        }
    }
    input.error {
        border-color: #de4040;
    }
</style>