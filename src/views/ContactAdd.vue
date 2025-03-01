<template>
    <div v-if="contact" class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactAddForm :contact="contact" @submit:contact="createContact" />
        <p>{{ message }}</p>
    </div>
</template>
<script>
import ContactAddForm from "@/components/ContactAddForm.vue";
import ContactService from "@/services/contact.service";
export default {
    components: {
        ContactAddForm,
    },
    props: {
        id: { type: String, required: true },
    },
    data() {
        return {
            contact: {
                name: "",
                phone: "",
                email: "",
            },
            message: "",
        };
    },
    methods: {
        async createContact(data) {
            try {
                await ContactService.create(data);
                alert('Liên hệ được tạo thành công.');
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
            }
        },
    }, 
};
</script>