<template>
  <div class="vendor-list">
    <h2 class="vendor-list-title">Vendor List</h2>

    <div v-if="vendorStore.loading">Loading vendors...</div>

    <div v-else-if="vendorStore.error" class="error">
      {{ vendorStore.error }}
    </div>

    <div v-else-if="vendorStore.vendors.length === 0" class="no-vendors">
      No vendors found. Add your first vendor!
    </div>

    <div v-else class="table-scroll">
      <table class="vendors-table">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Name</th>
            <th scope="col">Contact Person</th>
            <th scope="col">Email</th>
            <th scope="col">Partner Type</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="vendor in vendorStore.vendors" :key="vendor.id">
            <td>{{ vendor.id }}</td>
            <td>{{ vendor.name }}</td>
            <td>{{ vendor.contact_person }}</td>
            <td>{{ vendor.email }}</td>
            <td>{{ vendor.partner_type }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted } from "vue";
import { useVendorStore } from "../stores/vendorStore";

const vendorStore = useVendorStore();

onMounted(() => {
  vendorStore.fetchVendors();
});
</script>

<style scoped>

/* Layout */
.vendor-list {
  margin-top: var(--space-lg);
  width: 100%;
}

.vendor-list-title {
  text-align: left;
  margin-bottom: var(--space-md);
}

/* Table */
.vendors-table {
  width: 100%;
  border-collapse: collapse;
  background: var(--color-surface);
  border-radius: var(--radius-md);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
  color: var(--color-text);
}

.vendors-table th {
  text-align: left;
  padding: var(--space-sm) var(--space-md);
  background: var(--color-primary);
  color: #fff;
  font-weight: 600;
}

.vendors-table td {
  padding: var(--space-sm) var(--space-md);
  border-bottom: 1px solid var(--color-border);
}

/* Zebra striping */
.vendors-table tbody tr:nth-child(even) {
  background-color: var(--table-row-alt, #f9fafb);
}

/* Hover state */
.vendors-table tbody tr:hover {
  background-color: var(--table-row-hover, #eef2ff);
}

/* Focus state */
.vendors-table tbody tr:focus-within {
  outline: 2px solid var(--color-primary);
}

/* Error */
.error {
  color: red;
  padding: var(--space-sm);
}

/* Empty state */
.no-vendors {
  padding: var(--space-lg);
  text-align: center;
  color: #6b7280;
  border: 2px dashed var(--color-border);
  border-radius: var(--radius-md);
  background: var(--color-surface);
}

/* Mobile scroll */
@media (max-width: 600px) {
  .table-scroll {
    overflow-x: auto;
  }

  .vendors-table {
    min-width: 600px;
  }
}

</style>