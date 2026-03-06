<template>
  <div class="app-container">
    <header class="header">
      <div class="header-content">
        <h1>Trusted Vendor Portal</h1>

        <button class="theme-toggle" @click="toggleTheme">
          <span class="theme-icon">
            {{ isDark ? "☀️" : "🌙" }}
          </span>

          <span class="theme-label">
            {{ isDark ? "Light Mode" : "Dark Mode" }}
          </span>
        </button>
      </div>
    </header>

    <main>
      <div class="content-layout">
        <VendorForm />
        <VendorList />
      </div>
    </main>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import VendorForm from "./components/VendorForm.vue";
import VendorList from "./components/VendorList.vue";

const isDark = ref(false);

const toggleTheme = () => {
  isDark.value = !isDark.value;

  document.documentElement.setAttribute(
    "data-theme",
    isDark.value ? "dark" : "light",
  );
};

onMounted(() => {
  document.documentElement.setAttribute("data-theme", "light");
});
</script>

<style>
/* Reset */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

/* Page */
body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  background-color: #f4f4f4;
  transition: background-color 0.25s ease;
}

/* App container */
.app-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

@media (max-width: 768px) {
  .app-container {
    padding: 16px;
  }
}

/* Header */
.header {
  padding: 20px 0;
  margin-bottom: 20px;
  border-bottom: 2px solid #eee;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header h1 {
  color: #2c3e50;
}

/* Theme toggle */
.theme-toggle {
  display: flex;
  align-items: center;
  gap: 6px;
  background: transparent;
  border: none;
  color: black;
  cursor: pointer;
  font-size: 16px;
  padding: 6px 10px;
  border-radius: 6px;
  -webkit-tap-highlight-color: transparent;
}

/* Hover only on devices */
@media (hover: hover) and (pointer: fine) {
  .theme-toggle:hover {
    background-color: var(--color-primary);
  }
}

/* For mobile */
.theme-toggle:active {
  background-color: var(--color-primary);
}

.theme-icon {
  font-size: 18px;
}

.theme-label {
  color: black;
}

/* Layout */
.content-layout {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 30px;
}

@media (min-width: 1024px) {
  .content-layout {
    flex-direction: row;
    align-items: flex-start;
    justify-content: center;
  }

  .content-layout > * {
    flex: 1;
  }
}

/* For dark mode */
[data-theme="dark"] body {
  background-color: #121212;
  color: #eee;
}

[data-theme="dark"] .header {
  border-bottom: 2px solid #444;
}

[data-theme="dark"] .header h1 {
  color: #fff;
}

[data-theme="dark"] .theme-label {
  color: #fff;
}
</style>
