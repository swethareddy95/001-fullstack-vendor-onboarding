<template>
  <div class="vendor-form">
    <h2>Add New Vendor</h2>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="name">Name:</label>
        <input
          id="name"
          v-model="form.name"
          type="text"
          required
          placeholder="Company name"
        />
      </div>

      <div class="form-group">
        <label for="contactPerson">Contact Person:</label>
        <input
          id="contactPerson"
          v-model="form.contact_person"
          type="text"
          required
          placeholder="Contact person name"
        />
      </div>

      <div class="form-group">
        <label for="email">Email:</label>
        <input
          id="email"
          v-model="form.email"
          type="email"
          required
          placeholder="contact@example.com"
        />
      </div>

      <div class="form-group">
        <label for="partnerType">Partner Type:</label>
        <select id="partnerType" v-model="form.partner_type" required>
          <option value="Supplier">Supplier</option>
          <option value="Partner">Partner</option>
        </select>
      </div>

      <div class="form-actions">
        <button type="submit" :disabled="isSubmitting || vendorStore.loading">
          {{ isSubmitting ? "Submitting..." : "Add Vendor" }}
        </button>
        <div v-if="vendorStore.error" class="error-message">
          {{ vendorStore.error }}
        </div>
        <div v-if="success" class="success-message">
          Vendor added successfully!
        </div>
      </div>
    </form>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref } from "vue";
import { useVendorStore } from "../stores/vendorStore";
import type { Vendor } from "../types/Vendor";

const vendorStore = useVendorStore();

const form = reactive<Vendor>({
  name: "",
  contact_person: "",
  email: "",
  partner_type: "Supplier",
});

const success = ref(false);

const resetForm = () => {
  form.name = "";
  form.contact_person = "";
  form.email = "";
  form.partner_type = "Supplier";
};

const isSubmitting = ref(false);

const submitForm = async () => {
  if (isSubmitting.value) return;

  isSubmitting.value = true;
  success.value = false;

  try {
    await vendorStore.addVendor({ ...form });

    success.value = true;

    setTimeout(() => {
      resetForm();
      success.value = false;

      isSubmitting.value = false; //allow submission again after reset
    }, 2000);
  } catch (err) {
    isSubmitting.value = false;
  }
};
</script>

<style scoped>
.vendor-form {
  width: 100%;
  background: var(--color-surface);
  padding: var(--space-lg);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-sm);
  color: var(--color-text);
}

.vendor-form h2 {
  margin-bottom: var(--space-md);
}

/* Form layout */
.form-group {
  margin-bottom: var(--space-md);
}

.form-group label {
  display: block;
  font-weight: 600;
  color: var(--color-text);
  margin-bottom: var(--space-sm);
}

/* Inputs */
.form-group input,
.form-group select {
  width: 100%;
  padding: var(--space-sm);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  font-size: var(--font-size-base);
  background: var(--color-surface);
  color: var(--color-text);
}

/* Focus state */
.form-group input:focus,
.form-group select:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.2);
}

/* Actions */
.form-actions {
  margin-top: var(--space-md);
}

/* Button */
button {
  background: var(--color-primary);
  color: white;
  padding: var(--space-sm) var(--space-md);
  border: none;
  border-radius: var(--radius-md);
  cursor: pointer;
  font-weight: 600;
}

@media (hover: hover) {
  button:hover {
    background: var(--color-primary-hover);
  }
}

button:disabled {
  background: #cbd5e1;
  cursor: not-allowed;
}

/* Messages */
.error-message {
  color: #dc2626;
  margin-top: var(--space-sm);
}

.success-message {
  color: #16a34a;
  margin-top: var(--space-sm);
}
</style>
