<template>
  <div class="page">
    <ColumnItem title="处理">
      <el-form :model="vm" label-width="1rem">
        <el-form-item label="操作：" prop="prop1">
          <el-radio-group v-model="vm.prop1">
            <el-radio :label="1">静音</el-radio>
            <el-radio :label="2">取消静音</el-radio>
            <el-radio :label="3">复位</el-radio>
            <el-radio :label="4">断路</el-radio>
          </el-radio-group>
        </el-form-item>

        <el-row>
          <el-col :span="12">
            <el-form-item label="处理人：" prop="prop2">
              <el-input v-model="vm.prop2" clearable></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="联系电话：" prop="prop3">
              <el-input v-model="vm.prop3" clearable></el-input>
            </el-form-item>
          </el-col>
        </el-row>

        <el-form-item label="处理说明：" prop="prop4" class="textarea-item">
          <el-input type="textarea" rows="6" v-model="vm.prop4" clearable></el-input>
        </el-form-item>

        <el-form-item label="上传图片：" prop="prop5" class="textarea-item">
          <el-upload
            action="https://jsonplaceholder.typicode.com/posts/"
            list-type="picture-card"
            :file-list="fileList"
          >
            <i class="el-icon-plus"></i>

            <div slot="file" slot-scope="{file}">
              <img class="el-upload-list__item-thumbnail" :src="file.url" alt />
              <span class="el-upload-list__item-actions" style="opacity:1;">
                <span style="display:inline-block">
                  <i
                    @click="handlePreview(file)"
                    class="el-icon-zoom-in"
                    style="color:rgba(255,255,255,.7)"
                  ></i>
                </span>
                <span style="display:inline-block">
                  <i
                    class="el-icon-delete"
                    @click="handleRemove(file)"
                    style="color:rgba(255,255,255,.7)"
                  ></i>
                </span>
              </span>
            </div>
          </el-upload>
        </el-form-item>

      </el-form>

      <div class="item" style="text-align:right;padding-top:.3rem">
        <a class="btn btn-primary" @click="onConfirm">确认</a>
        <a class="btn" @click="onCancel">取消</a>
      </div>

    </ColumnItem>
  </div>
</template>

<script>
export default {
  data() {
    return {
      vm: {
        prop1: 1,
        prop2: 1,
      },

      dialogVisible: false,
      dialogImageUrl: "",

      fileList: [
        {
          name: "food.jpeg",
          url:
            "https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100",
        },
        {
          name: "food2.jpeg",
          url:
            "https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100",
        },
      ],
    };
  },

  methods: {
    onConfirm() {
      this.$emit("confirm");
    },

    onCancel() {
      this.$emit("cancel");
    },

    handlePreview(file) {
      this.dialogImageUrl = file.url;
      this.dialogVisible = true;

      this.$modal({
        placement: "center",
        width: "4rem",
        height: "4rem",
        component: {
          render: () => <img src={file.url} style="max-width:100%;" />,
        },
      });
    },

    handleRemove(file) {
      this.fileList.splice(this.fileList.indexOf(file), 1);
    },
  },
};
</script>

<style scoped lang="scss">
.item {
  margin-bottom: 0.24rem;
  font-size: 0.14rem;

  &:last-child {
    margin-bottom: 0;
  }

  &::after {
    content: "";
    height: 0;
    display: table;
    clear: both;
  }

  .el-radio-group {
    margin-left: 0.2rem;
  }
}
</style>

<style lang="scss">
.textarea-item {
  .el-form-item__label {
    height: 0.3rem;
    line-height: 0.3rem;
  }
}
</style>