<template>
    <div class="theme-switcher">
        <div class="dropdown dropdown-left">
            <label tabindex="0" class="btn m-1">
                <i class='bx bxs-palette bx-sm'></i>
            </label>
            <ul tabindex="0" class="dropdown-content menu p-2 shadow bg-base-100 rounded-box w-52">
                <li v-for="(theme, index) in themes" :key="index" class="theme-item" @click="changeTheme(index)">
                    <a>{{ theme }}</a>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ThemeSwitcher',
    data() {
        return {
            themes: ['cupcake', 'dark', 'light', 'bumblebee', 'synthwave', 'halloween', 'fantasy', 'dracula', 'aqua', 'luxury', 'night'],
        }
    },
    created() {
        const savedTheme = localStorage.getItem('theme');
        if (savedTheme) {
            document.querySelector("html").setAttribute("data-theme", savedTheme);
        }
    },
    methods: {
        changeTheme(index) {
            const selectedTheme = this.themes[index];
            document.querySelector("html").setAttribute("data-theme", selectedTheme);
            localStorage.setItem('theme', selectedTheme);
        }
    }
}
</script>