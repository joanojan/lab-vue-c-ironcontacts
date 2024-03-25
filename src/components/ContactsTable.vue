<script setup>
import { inject } from 'vue'

const contacts = inject('contacts')
</script>

<style scoped>
table {
    color: white;
}
th {
        background-color: rgb(38, 36, 159);
}
td {
    text-align: center;
    background-color: rgb(38, 76, 63);
}
.popularity, .name {
    width: 200px;
}
img {
    width: 110px;
}
</style>