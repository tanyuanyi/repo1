<template>
    <div>
        <quill-editor class="editor" ref="myTextEditor" v-model="value" :options="editorOption" @change="onEditorChange($event)">
        </quill-editor>
    </div>
</template>

<script>
export default {
    props: ["content"],
    data() {
        return {
            value: null,
            editorOption: {
                modules: {
                    toolbar: [
                        ["bold", "italic", "underline", "strike"], // 加粗 斜体 下划线 删除线
                        ["blockquote", "code-block"], // 引用  代码块
                        [{ header: 1 }, { header: 2 }], // 1、2 级标题
                        [{ list: "ordered" }, { list: "bullet" }], // 有序、无序列表
                        [{ script: "sub" }, { script: "super" }], // 上标/下标
                        [{ indent: "-1" }, { indent: "+1" }], // 缩进
                        // [{'direction': 'rtl'}],                         // 文本方向
                        [{ size: ["small", false, "large", "huge"] }], // 字体大小
                        [{ header: [1, 2, 3, 4, 5, 6, false] }], // 标题
                        [{ color: [] }, { background: [] }], // 字体颜色、字体背景颜色
                        [{ font: [] }], // 字体种类
                        [{ align: [] }], // 对齐方式
                        ["clean"], // 清除文本格式
                        ["link", "image", "video"] // 链接、图片、视频
                    ], //工具菜单栏配置
                },
                placeholder: '请在这里添加内容', //提示
                readyOnly: false, //是否只读
                theme: 'snow', //主题 snow/bubble
                syntax: true, //语法检测
            }
        }
    },
    mounted() {

    },
    watch: {
        content: {
            handler: function(){
                this.value = this.content;
            },
            immediate: true
        }
    },
    methods: {
        onEditorChange(editor) {    // 值发生变化
            this.value = editor.html;
            this.$emit('update:content', editor.html);
        },
    },
};
</script>