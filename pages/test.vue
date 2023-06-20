<template>
    <main>
        <ContentDoc v-slot="{ doc }">
            <!-- <pre>{{ doc }}</pre> -->
            <h1>{{ doc.title }}</h1>
            <ContentRenderer :value="doc" />
        </ContentDoc>
        <h3>Table content</h3>

        <!-- <div class="markdown-table"> -->
        <div>
            <ContentRenderer :value="table">
                <h1>{{ table.title }}</h1>
                <ContentRendererMarkdown :value="table" />
            </ContentRenderer>
        </div>
    </main>
</template>
  

<script setup lang="ts">

const contentQuery = await queryContent('test').findOne()
const table = contentQuery.body.children.find(child => child.tag === 'table')

console.log("🚀 ~ file: test.vue:16 ~ table:", table)
console.log("🚀 ~ file: test.vue:15 ~ contentQuery:", contentQuery)

</script>

<style>
.markdown-table {
    border: 1px solid #ccc;
    border-collapse: collapse;
    width: 100%;
}

.markdown-table th,
.markdown-table td {
    padding: 8px;
    text-align: left;
    border: 1px solid #ccc;
}

.markdown-table th {
    background-color: #f2f2f2;
}

.markdown-table tr:nth-child(odd) {
    background-color: #f8f8f8;
}
</style>