<!--<template>-->
<!--  <div>-->
<!--    <n-card :bordered="false" class="mt-2 proCard">-->
<!--      <BasicTable-->
<!--        ref="actionRef"-->
<!--        :columns="columns"-->
<!--        :request="loadDataTable"-->
<!--        :row-key="(row) => row.id"-->
<!--        :tableToolbarRight="false"-->
<!--      >-->
<!--        <template #tableTitle>-->
<!--          <n-space :inline="true" align="center">-->
<!--            <j-label label="内容类型" input-size="medium">-->
<!--              <j-dict-select-->
<!--                dict-type="CONTENT_TYPE"-->
<!--                v-model:value="params.type"-->
<!--                placeholder="内容类型"-->
<!--                clearable-->
<!--                @update:value="reloadTable"-->
<!--              />-->
<!--            </j-label>-->
<!--            <j-label label="内容标题" input-size="medium">-->
<!--              <n-input v-model:value="params.title" placeholder="内容标题" />-->
<!--            </j-label>-->
<!--            <n-space :inline="true" align="center">-->
<!--            <n-button type="primary" @click="reloadTable()">-->
<!--              <template #icon>-->
<!--                <n-icon :component="getIconComponentByName('SearchOutline')" />-->
<!--              </template>-->
<!--              查询-->
<!--            </n-button>-->
<!--            <n-button @click="resetParams">-->
<!--              <template #icon>-->
<!--                <n-icon :component="getIconComponentByName('RefreshOutline')" />-->
<!--              </template>-->
<!--              重置-->
<!--            </n-button>-->
<!--            <n-button-->
<!--              v-permission="{action: 'config:content:add'}"-->
<!--              type="primary"-->
<!--              @click="handleAdd()"-->
<!--            >-->
<!--              <template #icon>-->
<!--                <n-icon :component="getIconComponentByName('PlusOutlined')" />-->
<!--              </template>-->
<!--              新增-->
<!--            </n-button>-->
<!--            <n-button-->
<!--              v-permission="{action: 'config:content:import'}"-->
<!--              type="primary"-->
<!--              :disabled="Number(useSaas.getSaasId) < 200000"-->
<!--              @click="showImportConfig()"-->
<!--            >-->
<!--              <template #icon>-->
<!--                <n-icon :component="getIconComponentByName('DownloadOutline')" />-->
<!--              </template>-->
<!--              导入平台宣教配置-->
<!--            </n-button>-->
<!--            </n-space>-->
<!--           </n-space>-->
<!--        </template>-->
<!--      </BasicTable>-->
<!--    </n-card>-->

<!--    <n-drawer-->
<!--      v-model:show="drawerShowFlag"-->
<!--      :default-width="800"-->
<!--      resizable-->
<!--      @after-leave="drawerClosed"-->
<!--    >-->
<!--      <n-drawer-content closable :title="richTextTitle" :native-scrollbar="false">-->
<!--        <n-form-->
<!--          ref="formRef"-->
<!--          :label-width="100"-->
<!--          :model="richText"-->
<!--          :rules="rules"-->
<!--          label-placement="top"-->
<!--        >-->
<!--&lt;!&ndash;          <n-form-item label="租户名称" path="saasId">&ndash;&gt;-->
<!--&lt;!&ndash;            <n-select&ndash;&gt;-->
<!--&lt;!&ndash;              v-model:value="richText.saasId"&ndash;&gt;-->
<!--&lt;!&ndash;              :disabled="editFlag !== 'add'"&ndash;&gt;-->
<!--&lt;!&ndash;              :options="saasList"&ndash;&gt;-->
<!--&lt;!&ndash;              filterable&ndash;&gt;-->
<!--&lt;!&ndash;              label-field="name"&ndash;&gt;-->
<!--&lt;!&ndash;              placeholder="选择租户"&ndash;&gt;-->
<!--&lt;!&ndash;              value-field="id"&ndash;&gt;-->
<!--&lt;!&ndash;            />&ndash;&gt;-->
<!--&lt;!&ndash;          </n-form-item>&ndash;&gt;-->
<!--          <n-form-item label="标题" path="title">-->
<!--            <n-input v-model:value="richText.title" placeholder="请输入标题" />-->
<!--          </n-form-item>-->
<!--          <n-form-item label="渠道编码" path="appCode">-->
<!--            <j-dict-select-->
<!--              dict-type="CHANNEL_CODE"-->
<!--              v-model:value="richText.appCode"-->
<!--              placeholder="选择渠道编码"-->
<!--              filterable-->
<!--            />-->
<!--          </n-form-item>-->
<!--          <n-form-item label="用户终端" path="userClientType">-->
<!--            <j-dict-select-->
<!--              dict-type="USER_CLIENT_TYPE"-->
<!--              v-model:value="richText.userClientType"-->
<!--              placeholder="选择用户终端"-->
<!--              filterable-->
<!--              @getChildType="(typeList) => {richText.userClientChildType = typeList[0]}"-->
<!--              @update:value="() => {richText.terminalType = null}"-->
<!--            />-->
<!--          </n-form-item>-->
<!--          <n-form-item label="物理终端" v-show="richText.userClientType" path="terminalType">-->
<!--            <j-dict-select-->
<!--              v-model:value="richText.terminalType"-->
<!--              :dict-type="richText.userClientChildType"-->
<!--              placeholder="选择物理终端"-->
<!--              filterable-->
<!--            />-->
<!--          </n-form-item>-->
<!--          <n-form-item label="内容分类" path="type">-->
<!--            <j-dict-select-->
<!--              dict-type="CONTENT_TYPE"-->
<!--              v-model:value="richText.type"-->
<!--              placeholder="选择内容分类"-->
<!--              filterable-->
<!--            />-->
<!--          </n-form-item>-->
<!--          <n-form-item label="文件类型" path="fileType">-->
<!--            <j-dict-select-->
<!--              dict-type="FILE_TYPE"-->
<!--              v-model:value="richText.fileType"-->
<!--              placeholder="选择文件类型"-->
<!--              filterable-->
<!--            />-->
<!--          </n-form-item>-->
<!--          <n-form-item v-if="richText.fileType === 'VIDEO'" label="视频URL：" path="url">-->
<!--            <n-input v-model:value="richText.url" placeholder="请输入视频URL" />-->
<!--          </n-form-item>-->
<!--          <n-form-item v-if="richText.fileType === 'RICH_TEXT'" label="内容：" path="content">-->
<!--            <j-wang-editor :update-path="FileDirEnum.CONTENT_FILE" v-model:html="richText.content" />-->
<!--          </n-form-item>-->
<!--        </n-form>-->
<!--        <template #footer>-->
<!--          <n-space>-->
<!--            <n-button @click="drawerShowFlag = false">-->
<!--              取消-->
<!--            </n-button>-->
<!--            <n-button type="primary" @click="saveBtn">-->
<!--              确定-->
<!--            </n-button>-->
<!--          </n-space>-->
<!--        </template>-->
<!--      </n-drawer-content>-->
<!--    </n-drawer>-->



<!--    <basicModal ref="roleModalRef" style="width: 1000px" @register="modalRegister" @on-ok="okModal">-->
<!--      <BasicTable-->
<!--        ref="importActionRef"-->
<!--        :columns="importColumns"-->
<!--        :request="importLoadDataTable"-->
<!--        :row-key="(row) => row.id"-->
<!--        :pagination="false"-->
<!--        :tableToolbarRight="false"-->
<!--        :scroll-x="800"-->
<!--        @update:checked-row-keys="handleCheck"-->
<!--      />-->
<!--    </basicModal>-->
<!--  </div>-->
<!--</template>-->

<!--<script lang="ts" setup>-->
<!--import { BasicTable } from "@/components/Table";-->
<!--import { baseColumns, getColumns } from './columns';-->
<!--import {-->
<!--  deleteRichText,-->
<!--  getPlatformConfig,-->
<!--  getRichTextList, importPlatformConfig,-->
<!--  saveRichText,-->
<!--  changeStatus,-->
<!--} from '@/api/configManage/contentManage';-->
<!--import { useSaasSettingStore } from "@/store/modules/saasSetting";-->
<!--import { JWangEditor } from "@/components/JWangEditor";-->
<!--import { useDialog, useMessage } from "naive-ui";-->
<!--import { resetObj } from "@/utils/dataUtil";-->
<!--import { FileDirEnum } from "@/hooks/useUpload";-->
<!--import { unref, ref, reactive, onMounted, h, computed } from 'vue';-->
<!--import { getIconComponentByName } from '@/utils/iconsUtil';-->
<!--import { useModal } from '@/components/Modal';-->
<!--import {JLabel} from "@/components/JLabel";-->

<!--const useSaas = useSaasSettingStore();-->
<!--const message = useMessage();-->
<!--const dialog = useDialog();-->

<!--const columns = getColumns({-->
<!--  actions: {-->
<!--    statusBtn: (record) => {-->
<!--      resetObj(richText, record);-->
<!--      let title: string, type: string;-->

<!--      if ('' + richText.status === '1') {-->
<!--        richText.status = '0';-->
<!--        type = 'error';-->
<!--        title = `确定禁用【${richText.title}】吗? `;-->
<!--      } else {-->
<!--        richText.status = '1';-->
<!--        type = 'success';-->
<!--        title = `确定启用【${richText.title}】吗? `;-->
<!--      }-->

<!--      dialog[type]({-->
<!--        title: title,-->
<!--        type: 'success',-->
<!--        positiveText: '确定',-->
<!--        negativeText: '取消',-->
<!--        closable: false,-->
<!--        maskClosable: false,-->
<!--        onPositiveClick: () => {-->
<!--          changeStatus(richText).then(res => {-->
<!--            message.success('操作成功')-->
<!--            reloadTable();-->
<!--          })-->
<!--        }-->
<!--      });-->
<!--    },-->
<!--  },-->
<!--  actionList: [-->
<!--    {-->
<!--      name: "编辑",-->
<!--      text: true,-->
<!--      permissionCode: "config:content:update",-->
<!--      onClick: (record: any) => {-->
<!--        richTextTitle.value = "编辑";-->
<!--        editFlag.value = "edit";-->
<!--        resetObj(richText, record);-->
<!--        drawerShowFlag.value = true-->
<!--      }-->
<!--    },-->
<!--    {-->
<!--      name: "删除",-->
<!--      text: true,-->
<!--      permissionCode: "config:content:delete",-->
<!--      onClick: (record: any) => {-->
<!--        dialog.error({-->
<!--          title: "提示",-->
<!--          content: `您确定想删除此文本吗?`,-->
<!--          positiveText: "确定",-->
<!--          negativeText: "取消",-->
<!--          onPositiveClick: () => {-->
<!--            deleteRichText(record.id).then(res => {-->
<!--              reloadTable();-->
<!--              message.success("删除成功");-->
<!--            });-->
<!--          },-->
<!--          onNegativeClick: () => {-->
<!--            // message.error('已取消');-->
<!--          }-->
<!--        });-->
<!--      }-->
<!--    }-->
<!--  ]-->
<!--})-->


<!--const actionRef = ref();-->
<!--const editFlag = ref("add");-->

<!--const richTextTitle = ref("添加");-->
<!--const drawerShowFlag = ref(false)-->

<!--const drawerClosed = () => {-->
<!--  reloadTable();-->
<!--  drawerShowFlag.value = false-->
<!--}-->


<!--const richText = reactive({-->
<!--  id: "",-->
<!--  platformCode: "",-->
<!--  title: "",-->
<!--  saasId: "",-->
<!--  appCode: "",-->
<!--  type: "",-->
<!--  userClientType: "",-->
<!--  terminalType: "",-->
<!--  fileType: "",-->
<!--  url: "",-->
<!--  content: "",-->
<!--});-->

<!--const rules = computed(() => {-->
<!--  const base = {-->
<!--    saasId: {-->
<!--      required: true,-->
<!--      message: "请选择租户",-->
<!--      trigger: "blur"-->
<!--    },-->
<!--    title: {-->
<!--      required: true,-->
<!--      message: "请输入标题",-->
<!--      trigger: "blur"-->
<!--    },-->
<!--    appCode: {-->
<!--      required: true,-->
<!--      message: "选择渠道编码",-->
<!--      trigger: "blur"-->
<!--    },-->
<!--    userClientType: {-->
<!--      required: true,-->
<!--      message: "选择用户终端",-->
<!--      trigger: "blur"-->
<!--    },-->
<!--    terminalType: {-->
<!--      required: true,-->
<!--      message: "选择物理终端",-->
<!--      trigger: "blur"-->
<!--    },-->
<!--    type: {-->
<!--      required: true,-->
<!--      message: "选择内容分类",-->
<!--      trigger: "blur"-->
<!--    },-->
<!--    fileType: {-->
<!--      required: true,-->
<!--      message: "选择文件类型",-->
<!--      trigger: "blur"-->
<!--    },-->
<!--  }-->
<!--  if (richText.type === "VIDEO") {-->
<!--    return {-->
<!--      ...base,-->
<!--      url: {-->
<!--        required: true,-->
<!--        message: "请输入视频URL",-->
<!--        trigger: "blur"-->
<!--      }-->
<!--    }-->
<!--  } else if (richText.type === "RICH_TEXT") {-->
<!--    return {-->
<!--      ...base,-->
<!--      content: {-->
<!--        required: true,-->
<!--        message: "请填写内容",-->
<!--        trigger: "blur"-->
<!--      }-->
<!--    }-->
<!--  }-->
<!--  return base-->
<!--})-->

<!--const params = reactive({-->
<!--  platformCode: useSaas.getPlatformCode,-->
<!--  saasId: "",-->
<!--  type: null,-->
<!--  title: "",-->
<!--  userClientType: ""-->
<!--});-->
<!--// const loadDataTable = async (res: any) => {-->
<!--//   if (!params.saasId) return-->
<!--//   // res.size = res.pageSize-->
<!--//   const userPage = await getRichTextList({-->
<!--//     ...unref(params),-->
<!--//     ...res-->
<!--//   });-->
<!--//   return {-->
<!--//     list: userPage.data,-->
<!--//     page: Number(userPage.page),-->
<!--//     pageCount: Number(userPage.pageCount),-->
<!--//     pageSize: Number(userPage.pageSize),-->
<!--//     itemCount: Number(userPage.totalNumber)-->
<!--//   };-->
<!--// };-->

<!--const staticData = [-->
<!--  {-->
<!--    id: 1,-->
<!--    title: '胃肠外科手术指南',-->
<!--    platformCode: 'PLATFORM_001',-->
<!--    type: 'SURGERY_GUIDE',-->
<!--    appCode: 'APP_001',-->
<!--    userClientType: 'MOBILE',-->
<!--    terminalType: 'ANDROID',-->
<!--    fileType: 'PDF',-->
<!--    createdDate: '2023-10-01 10:00:00',-->
<!--    status: '1',-->
<!--  },-->
<!--  {-->
<!--    id: 2,-->
<!--    title: '胃肠道疾病诊断',-->
<!--    platformCode: 'PLATFORM_002',-->
<!--    type: 'DIAGNOSIS',-->
<!--    appCode: 'APP_002',-->
<!--    userClientType: 'WEB',-->
<!--    terminalType: 'CHROME',-->
<!--    fileType: 'DOC',-->
<!--    createdDate: '2023-10-02 11:00:00',-->
<!--    status: '0',-->
<!--  },-->
<!--  {-->
<!--    id: 3,-->
<!--    title: '胃肠外科术后护理',-->
<!--    platformCode: 'PLATFORM_003',-->
<!--    type: 'POST_OP_CARE',-->
<!--    appCode: 'APP_003',-->
<!--    userClientType: 'DESKTOP',-->
<!--    terminalType: 'WINDOWS',-->
<!--    fileType: 'VIDEO',-->
<!--    createdDate: '2023-10-03 12:00:00',-->
<!--    status: '1',-->
<!--  },-->
<!--  {-->
<!--    id: 4,-->
<!--    title: '胃肠道手术风险评估',-->
<!--    platformCode: 'PLATFORM_004',-->
<!--    type: 'RISK_ASSESSMENT',-->
<!--    appCode: 'APP_004',-->
<!--    userClientType: 'MOBILE',-->
<!--    terminalType: 'IOS',-->
<!--    fileType: 'PDF',-->
<!--    createdDate: '2023-10-04 13:00:00',-->
<!--    status: '0',-->
<!--  },-->
<!--  {-->
<!--    id: 5,-->
<!--    title: '胃肠道健康饮食指南',-->
<!--    platformCode: 'PLATFORM_005',-->
<!--    type: 'DIET_GUIDE',-->
<!--    appCode: 'APP_005',-->
<!--    userClientType: 'WEB',-->
<!--    terminalType: 'FIREFOX',-->
<!--    fileType: 'DOC',-->
<!--    createdDate: '2023-10-05 14:00:00',-->
<!--    status: '1',-->
<!--  },-->
<!--  {-->
<!--    id: 6,-->
<!--    title: '胃肠道疾病预防',-->
<!--    platformCode: 'PLATFORM_006',-->
<!--    type: 'PREVENTION',-->
<!--    appCode: 'APP_006',-->
<!--    userClientType: 'DESKTOP',-->
<!--    terminalType: 'LINUX',-->
<!--    fileType: 'VIDEO',-->
<!--    createdDate: '2023-10-06 15:00:00',-->
<!--    status: '0',-->
<!--  },-->
<!--  {-->
<!--    id: 7,-->
<!--    title: '胃肠道手术后康复',-->
<!--    platformCode: 'PLATFORM_007',-->
<!--    type: 'REHABILITATION',-->
<!--    appCode: 'APP_007',-->
<!--    userClientType: 'MOBILE',-->
<!--    terminalType: 'ANDROID',-->
<!--    fileType: 'PDF',-->
<!--    createdDate: '2023-10-07 16:00:00',-->
<!--    status: '1',-->
<!--  },-->
<!--  {-->
<!--    id: 8,-->
<!--    title: '胃肠道疾病药物治疗',-->
<!--    platformCode: 'PLATFORM_008',-->
<!--    type: 'MEDICATION',-->
<!--    appCode: 'APP_008',-->
<!--    userClientType: 'WEB',-->
<!--    terminalType: 'SAFARI',-->
<!--    fileType: 'DOC',-->
<!--    createdDate: '2023-10-08 17:00:00',-->
<!--    status: '0',-->
<!--  },-->
<!--  {-->
<!--    id: 9,-->
<!--    title: '胃肠道手术并发症管理',-->
<!--    platformCode: 'PLATFORM_009',-->
<!--    type: 'COMPLICATION_MANAGEMENT',-->
<!--    appCode: 'APP_009',-->
<!--    userClientType: 'DESKTOP',-->
<!--    terminalType: 'MACOS',-->
<!--    fileType: 'VIDEO',-->
<!--    createdDate: '2023-10-09 18:00:00',-->
<!--    status: '1',-->
<!--  },-->
<!--  {-->
<!--    id: 10,-->
<!--    title: '胃肠道疾病症状识别',-->
<!--    platformCode: 'PLATFORM_010',-->
<!--    type: 'SYMPTOM_IDENTIFICATION',-->
<!--    appCode: 'APP_010',-->
<!--    userClientType: 'MOBILE',-->
<!--    terminalType: 'IOS',-->
<!--    fileType: 'PDF',-->
<!--    createdDate: '2023-10-10 19:00:00',-->
<!--    status: '0',-->
<!--  },-->
<!--  {-->
<!--    id: 11,-->
<!--    title: '胃肠道手术技术进展',-->
<!--    platformCode: 'PLATFORM_011',-->
<!--    type: 'TECH_ADVANCEMENT',-->
<!--    appCode: 'APP_011',-->
<!--    userClientType: 'WEB',-->
<!--    terminalType: 'EDGE',-->
<!--    fileType: 'DOC',-->
<!--    createdDate: '2023-10-11 20:00:00',-->
<!--    status: '1',-->
<!--  },-->
<!--  {-->
<!--    id: 12,-->
<!--    title: '胃肠道疾病患者教育',-->
<!--    platformCode: 'PLATFORM_012',-->
<!--    type: 'PATIENT_EDUCATION',-->
<!--    appCode: 'APP_012',-->
<!--    userClientType: 'DESKTOP',-->
<!--    terminalType: 'WINDOWS',-->
<!--    fileType: 'VIDEO',-->
<!--    createdDate: '2023-10-12 21:00:00',-->
<!--    status: '0',-->
<!--  },-->
<!--  {-->
<!--    id: 13,-->
<!--    title: '胃肠道手术术前准备',-->
<!--    platformCode: 'PLATFORM_013',-->
<!--    type: 'PRE_OP_PREPARATION',-->
<!--    appCode: 'APP_013',-->
<!--    userClientType: 'MOBILE',-->
<!--    terminalType: 'ANDROID',-->
<!--    fileType: 'PDF',-->
<!--    createdDate: '2023-10-13 22:00:00',-->
<!--    status: '1',-->
<!--  },-->
<!--  {-->
<!--    id: 14,-->
<!--    title: '胃肠道疾病营养支持',-->
<!--    platformCode: 'PLATFORM_014',-->
<!--    type: 'NUTRITION_SUPPORT',-->
<!--    appCode: 'APP_014',-->
<!--    userClientType: 'WEB',-->
<!--    terminalType: 'CHROME',-->
<!--    fileType: 'DOC',-->
<!--    createdDate: '2023-10-14 23:00:00',-->
<!--    status: '0',-->
<!--  },-->
<!--  {-->
<!--    id: 15,-->
<!--    title: '胃肠道手术后并发症',-->
<!--    platformCode: 'PLATFORM_015',-->
<!--    type: 'POST_OP_COMPLICATIONS',-->
<!--    appCode: 'APP_015',-->
<!--    userClientType: 'DESKTOP',-->
<!--    terminalType: 'LINUX',-->
<!--    fileType: 'VIDEO',-->
<!--    createdDate: '2023-10-15 10:00:00',-->
<!--    status: '1',-->
<!--  },-->
<!--  {-->
<!--    id: 16,-->
<!--    title: '胃肠道疾病手术选择',-->
<!--    platformCode: 'PLATFORM_016',-->
<!--    type: 'SURGERY_SELECTION',-->
<!--    appCode: 'APP_016',-->
<!--    userClientType: 'MOBILE',-->
<!--    terminalType: 'IOS',-->
<!--    fileType: 'PDF',-->
<!--    createdDate: '2023-10-16 11:00:00',-->
<!--    status: '0',-->
<!--  },-->
<!--  {-->
<!--    id: 17,-->
<!--    title: '胃肠道手术后饮食管理',-->
<!--    platformCode: 'PLATFORM_017',-->
<!--    type: 'POST_OP_DIET',-->
<!--    appCode: 'APP_017',-->
<!--    userClientType: 'WEB',-->
<!--    terminalType: 'FIREFOX',-->
<!--    fileType: 'DOC',-->
<!--    createdDate: '2023-10-17 12:00:00',-->
<!--    status: '1',-->
<!--  },-->
<!--  {-->
<!--    id: 18,-->
<!--    title: '胃肠道疾病康复计划',-->
<!--    platformCode: 'PLATFORM_018',-->
<!--    type: 'REHAB_PLAN',-->
<!--    appCode: 'APP_018',-->
<!--    userClientType: 'DESKTOP',-->
<!--    terminalType: 'MACOS',-->
<!--    fileType: 'VIDEO',-->
<!--    createdDate: '2023-10-18 13:00:00',-->
<!--    status: '0',-->
<!--  },-->
<!--  {-->
<!--    id: 19,-->
<!--    title: '胃肠道手术后疼痛管理',-->
<!--    platformCode: 'PLATFORM_019',-->
<!--    type: 'PAIN_MANAGEMENT',-->
<!--    appCode: 'APP_019',-->
<!--    userClientType: 'MOBILE',-->
<!--    terminalType: 'ANDROID',-->
<!--    fileType: 'PDF',-->
<!--    createdDate: '2023-10-19 14:00:00',-->
<!--    status: '1',-->
<!--  },-->
<!--  {-->
<!--    id: 20,-->
<!--    title: '胃肠道疾病治疗方案',-->
<!--    platformCode: 'PLATFORM_020',-->
<!--    type: 'TREATMENT_PLAN',-->
<!--    appCode: 'APP_020',-->
<!--    userClientType: 'WEB',-->
<!--    terminalType: 'SAFARI',-->
<!--    fileType: 'DOC',-->
<!--    createdDate: '2023-10-20 15:00:00',-->
<!--    status: '0',-->
<!--  }-->
<!--];-->

<!--//静态数据-->
<!--const loadDataTable = async (res: any) => {-->
<!--  return {-->
<!--    list: staticData,-->
<!--    page: 1,-->
<!--    pageCount: 1,-->
<!--    pageSize: staticData.length,-->
<!--    itemCount: staticData.length-->
<!--  };-->
<!--};-->
<!--const reloadTable = () => {-->
<!--  actionRef.value.reload();-->
<!--};-->
<!--const resetParams = () => {-->
<!--  resetObj(params, {-->
<!--    saasId: params.saasId,-->
<!--    type: null,-->
<!--    name: null,-->
<!--    createdDate: null-->
<!--  });-->
<!--  reloadTable();-->
<!--};-->


<!--const handleAdd = () => {-->
<!--  richTextTitle.value = "添加";-->
<!--  editFlag.value = "add";-->

<!--  resetObj(richText);-->

<!--  richText.platformCode = useSaas.getPlatformCode;-->
<!--  drawerShowFlag.value = true-->
<!--};-->

<!--const formRef = ref();-->
<!--const saveBtn = () => {-->
<!--  formRef.value.validate((errors: boolean) => {-->
<!--    if (!errors) {-->
<!--      saveRichText(richText).then(res => {-->
<!--        console.log(res);-->
<!--        drawerShowFlag.value = false-->
<!--      })-->
<!--    }-->
<!--  });-->
<!--};-->

<!--const [modalRegister, { openModal, closeModal, setSubLoading }] = useModal({-->
<!--  title: '导入',-->
<!--});-->

<!--const importData = reactive({-->
<!--  saasId: params.saasId,-->
<!--  ids: []-->
<!--})-->
<!--const okModal = () => {-->
<!--  importData.saasId = params.saasId-->
<!--  importPlatformConfig(importData).then(res => {-->
<!--    console.log(res);-->
<!--    setSubLoading(false)-->
<!--    closeModal()-->
<!--    message.success('导入成功')-->
<!--    reloadTable()-->
<!--  })-->
<!--}-->

<!--const showImportConfig = () => {-->
<!--  importData.ids.clear()-->
<!--  openModal()-->
<!--  // importActionRef.value.reload();-->
<!--}-->
<!--const importActionRef = ref();-->
<!--const importColumns = [-->
<!--  {-->
<!--    type: 'selection',-->
<!--    disabled(row) {-->
<!--      return row.have === '1'-->
<!--    }-->
<!--  },-->
<!--  ...baseColumns,-->
<!--  {-->
<!--    title: '是否已经导入',-->
<!--    key: 'have',-->
<!--    render: (row) => {-->
<!--      return row.have == '1' ? '是' : '否'-->
<!--    }-->
<!--  }-->
<!--]-->

<!--const importLoadDataTable = async (res: any) => {-->
<!--  if (!params.saasId) return-->
<!--  // res.size = res.pageSize-->
<!--  const list = await getPlatformConfig({-->
<!--    platformId: useSaas.getPlatformId,-->
<!--    type: "3",-->
<!--    saasId: params.saasId-->
<!--  });-->
<!--  return {-->
<!--    list: list,-->
<!--  };-->
<!--};-->

<!--const handleCheck = (rowKeys) => {-->
<!--  importData.ids = rowKeys-->
<!--}-->

<!--onMounted(() => {-->
<!--  params.saasId = useSaas.getSaasId;-->
<!--  reloadTable();-->
<!--});-->

<!--</script>-->

<!--<style lang="less" scoped>-->

<!--</style>-->


<template>
  <div>
    <n-card :bordered="false" class="mt-2 proCard">
      <BasicTable
        ref="actionRef"
        :columns="columns"
        :request="loadDataTable"
        :row-key="(row) => row.id"
        :tableToolbarRight="false"
      >
        <template #tableTitle>
          <n-space :inline="true" align="center">
            <j-label label="内容类型" input-size="medium">
              <n-select
                v-model:value="params.type"
                :options="contentTypeOptions"
                placeholder="内容类型"
                clearable
                @update:value="reloadTable"
              />
            </j-label>
            <j-label label="内容标题" input-size="medium">
              <n-input v-model:value="params.title" placeholder="内容标题" />
            </j-label>
            <n-space :inline="true" align="center">
              <n-button type="primary" @click="reloadTable()">
                <template #icon>
                  <n-icon :component="getIconComponentByName('SearchOutline')" />
                </template>
                查询
              </n-button>
              <n-button @click="resetParams">
                <template #icon>
                  <n-icon :component="getIconComponentByName('RefreshOutline')" />
                </template>
                重置
              </n-button>
              <n-button
                v-permission="{action: 'config:content:add'}"
                type="primary"
                @click="handleAdd()"
              >
                <template #icon>
                  <n-icon :component="getIconComponentByName('PlusOutlined')" />
                </template>
                新增
              </n-button>
            </n-space>
          </n-space>
        </template>
      </BasicTable>
    </n-card>

    <n-drawer
      v-model:show="drawerShowFlag"
      :default-width="800"
      resizable
      @after-leave="drawerClosed"
    >
      <n-drawer-content closable :title="richTextTitle" :native-scrollbar="false">
        <n-form
          ref="formRef"
          :label-width="100"
          :model="richText"
          :rules="rules"
          label-placement="top"
        >
          <n-form-item label="标题" path="title">
            <n-input v-model:value="richText.title" placeholder="请输入标题" />
          </n-form-item>
          <n-form-item label="渠道编码" path="appCode">
            <j-dict-select
              dict-type="CHANNEL_CODE"
              v-model:value="richText.appCode"
              placeholder="选择渠道编码"
              filterable
            />
          </n-form-item>
          <n-form-item label="用户终端" path="userClientType">
            <j-dict-select
              dict-type="USER_CLIENT_TYPE"
              v-model:value="richText.userClientType"
              placeholder="选择用户终端"
              filterable
              @getChildType="(typeList) => {richText.userClientChildType = typeList[0]}"
              @update:value="() => {richText.terminalType = null}"
            />
          </n-form-item>
          <n-form-item label="物理终端" v-show="richText.userClientType" path="terminalType">
            <j-dict-select
              v-model:value="richText.terminalType"
              :dict-type="richText.userClientChildType"
              placeholder="选择物理终端"
              filterable
            />
          </n-form-item>
          <n-form-item label="内容分类" path="type">
            <n-select
              v-model:value="richText.type"
              :options="contentTypeOptions"
              placeholder="内容类型"
              clearable
            />
          </n-form-item>
          <n-form-item label="文件类型" path="fileType">
            <j-dict-select
              dict-type="FILE_TYPE"
              v-model:value="richText.fileType"
              placeholder="选择文件类型"
              filterable
            />
          </n-form-item>
          <n-form-item v-if="richText.fileType === 'VIDEO'" label="视频URL：" path="url">
            <n-input v-model:value="richText.url" placeholder="请输入视频URL" />
          </n-form-item>
          <n-form-item v-if="richText.fileType === 'RICH_TEXT'" label="内容：" path="content">
          </n-form-item>
        </n-form>
        <template #footer>
          <n-space>
            <n-button @click="drawerShowFlag = false">
              取消
            </n-button>
            <n-button type="primary" @click="saveBtn">
              确定
            </n-button>
          </n-space>
        </template>
      </n-drawer-content>
    </n-drawer>
  </div>
</template>

<script lang="ts" setup>
  import { BasicTable } from "@/components/Table";
  import { getColumns } from './columns';
  import { useSaasSettingStore } from "@/store/modules/saasSetting";
  import { useDialog, useMessage } from "naive-ui";
  import { resetObj } from "@/utils/dataUtil";
  import { unref, ref, reactive, onMounted, computed } from 'vue';
  import { getIconComponentByName } from '@/utils/iconsUtil';
  import { JLabel } from "@/components/JLabel";

  const useSaas = useSaasSettingStore();
  const message = useMessage();
  const dialog = useDialog();

  const contentTypeOptions = [
    { label: '平台服务协议', value: '平台服务协议' },
    { label: '平台隐私协议', value: '平台隐私协议' },
    { label: '宣教资料', value: '宣教资料' },
    { label: '操作手册', value: '操作手册' }
  ];

  const staticData = [
    {
      id: 1,
      saasId: 'SAAS_001',
      title: '平台服务协议 - 胃肠外科',
      platformCode: 'PLATFORM_001',
      type: '平台服务协议',
      appCode: 'APP_001',
      userClientType: '患者端',
      terminalType: '安卓',
      fileType: 'PDF',
      createdDate: '2023-10-01 10:00:00',
      status: '1',
    },
    {
      id: 2,
      saasId: 'SAAS_002',
      title: '平台隐私协议 - 胃肠外科',
      platformCode: 'PLATFORM_002',
      type: '平台隐私协议',
      appCode: 'APP_002',
      userClientType: '患者端',
      terminalType: 'Chrome',
      fileType: 'DOC',
      createdDate: '2023-10-02 11:00:00',
      status: '0',
    },
    {
      id: 3,
      saasId: 'SAAS_003',
      title: '宣教资料 - 胃肠外科',
      platformCode: 'PLATFORM_003',
      type: '宣教资料',
      appCode: 'APP_003',
      userClientType: '患者端',
      terminalType: 'Windows',
      fileType: '视频',
      createdDate: '2023-10-03 12:00:00',
      status: '1',
    },
    {
      id: 4,
      saasId: 'SAAS_004',
      title: '操作手册 - 胃肠外科',
      platformCode: 'PLATFORM_004',
      type: '操作手册',
      appCode: 'APP_004',
      userClientType: '患者端',
      terminalType: 'iOS',
      fileType: 'PDF',
      createdDate: '2023-10-04 13:00:00',
      status: '1',
    },
    {
      id: 5,
      saasId: 'SAAS_005',
      title: '平台服务协议 - 胃肠外科',
      platformCode: 'PLATFORM_005',
      type: '平台服务协议',
      appCode: 'APP_005',
      userClientType: '患者端',
      terminalType: 'Safari',
      fileType: 'DOC',
      createdDate: '2023-10-05 14:00:00',
      status: '0',
    },
    {
      id: 6,
      saasId: 'SAAS_006',
      title: '平台隐私协议 - 胃肠外科',
      platformCode: 'PLATFORM_006',
      type: '平台隐私协议',
      appCode: 'APP_006',
      userClientType: '患者端',
      terminalType: '安卓',
      fileType: 'PDF',
      createdDate: '2023-10-06 15:00:00',
      status: '1',
    },
    {
      id: 7,
      saasId: 'SAAS_007',
      title: '宣教资料 - 胃肠外科',
      platformCode: 'PLATFORM_007',
      type: '宣教资料',
      appCode: 'APP_007',
      userClientType: '桌面端',
      terminalType: 'Linux',
      fileType: '视频',
      createdDate: '2023-10-07 16:00:00',
      status: '1',
    },
    {
      id: 8,
      saasId: 'SAAS_008',
      title: '操作手册 - 胃肠外科',
      platformCode: 'PLATFORM_008',
      type: '操作手册',
      appCode: 'APP_008',
      userClientType: '网页端',
      terminalType: 'Edge',
      fileType: 'DOC',
      createdDate: '2023-10-08 17:00:00',
      status: '0',
    },
    {
      id: 9,
      saasId: 'SAAS_009',
      title: '平台服务协议 - 胃肠外科',
      platformCode: 'PLATFORM_009',
      type: '平台服务协议',
      appCode: 'APP_009',
      userClientType: '移动端',
      terminalType: 'iOS',
      fileType: 'PDF',
      createdDate: '2023-10-09 18:00:00',
      status: '1',
    },
    {
      id: 10,
      saasId: 'SAAS_010',
      title: '平台隐私协议 - 胃肠外科',
      platformCode: 'PLATFORM_010',
      type: '平台隐私协议',
      appCode: 'APP_010',
      userClientType: '桌面端',
      terminalType: 'Windows',
      fileType: '视频',
      createdDate: '2023-10-10 19:00:00',
      status: '0',
    },
    {
      id: 11,
      saasId: 'SAAS_011',
      title: '宣教资料 - 胃肠外科',
      platformCode: 'PLATFORM_011',
      type: '宣教资料',
      appCode: 'APP_011',
      userClientType: '网页端',
      terminalType: 'Chrome',
      fileType: 'DOC',
      createdDate: '2023-10-11 20:00:00',
      status: '1',
    },
    {
      id: 12,
      saasId: 'SAAS_012',
      title: '操作手册 - 胃肠外科',
      platformCode: 'PLATFORM_012',
      type: '操作手册',
      appCode: 'APP_012',
      userClientType: '移动端',
      terminalType: '安卓',
      fileType: 'PDF',
      createdDate: '2023-10-12 21:00:00',
      status: '1',
    },
    {
      id: 13,
      saasId: 'SAAS_013',
      title: '平台服务协议 - 胃肠外科',
      platformCode: 'PLATFORM_013',
      type: '平台服务协议',
      appCode: 'APP_013',
      userClientType: '桌面端',
      terminalType: 'Linux',
      fileType: '视频',
      createdDate: '2023-10-13 22:00:00',
      status: '0',
    },
    {
      id: 14,
      saasId: 'SAAS_014',
      title: '平台隐私协议 - 胃肠外科',
      platformCode: 'PLATFORM_014',
      type: '平台隐私协议',
      appCode: 'APP_014',
      userClientType: '网页端',
      terminalType: 'Safari',
      fileType: 'DOC',
      createdDate: '2023-10-14 23:00:00',
      status: '1',
    },
    {
      id: 15,
      saasId: 'SAAS_015',
      title: '宣教资料 - 胃肠外科',
      platformCode: 'PLATFORM_015',
      type: '宣教资料',
      appCode: 'APP_015',
      userClientType: '移动端',
      terminalType: 'iOS',
      fileType: 'PDF',
      createdDate: '2023-10-15 09:00:00',
      status: '1',
    }
  ];

  // 新增功能
  const addRecord = (record) => {
    const newId = staticData.length ? Math.max(...staticData.map(item => item.id)) + 1 : 1;
    staticData.push({ ...record, id: newId });
    message.success("新增成功");
    drawerShowFlag.value = false;
    reloadTable();
  };

  // 编辑功能
  const editRecord = (record) => {
    const index = staticData.findIndex(item => item.id === record.id);
    if (index !== -1) {
      staticData[index] = { ...record };
      message.success("编辑成功");
      reloadTable();
    }
  };

  // 删除功能
  const deleteRecord = (id) => {
    const index = staticData.findIndex(item => item.id === id);
    if (index !== -1) {
      staticData.splice(index, 1);
      message.success("删除成功");
      reloadTable();
    }
  };

  // 查询功能
  const queryRecords = (params) => {
    return staticData.filter(item => {
      return (!params.type || item.type === params.type) &&
        (!params.title || item.title.includes(params.title));
    });
  };

  // 修改 loadDataTable 函数以使用查询功能
  const loadDataTable = async (res: any) => {
    const filteredData = queryRecords(params);
    return {
      list: filteredData,
      page: 1,
      pageCount: 1,
      pageSize: filteredData.length,
      itemCount: filteredData.length
    };
  };

  const columns = getColumns({
    actions: {
      statusBtn: (record) => {
        resetObj(richText, record);
        let title: string, type: string;

        if ('' + richText.status === '1') {
          richText.status = '0';
          type = 'error';
          title = `确定禁用【${richText.title}】吗? `;
        } else {
          richText.status = '1';
          type = 'success';
          title = `确定启用【${richText.title}】吗? `;
        }

        dialog[type]({
          title: title,
          type: 'success',
          positiveText: '确定',
          negativeText: '取消',
          closable: false,
          maskClosable: false,
          onPositiveClick: () => {
            editRecord(richText);
          }
        });
      },
    },
    actionList: [
      {
        name: "编辑",
        text: true,
        permissionCode: "config:content:update",
        onClick: (record: any) => {
          richTextTitle.value = "编辑";
          editFlag.value = "edit";
          resetObj(richText, record);
          drawerShowFlag.value = true;
        }
      },
      {
        name: "删除",
        text: true,
        permissionCode: "config:content:delete",
        onClick: (record: any) => {
          dialog.error({
            title: "提示",
            content: `您确定想删除此文本吗?`,
            positiveText: "确定",
            negativeText: "取消",
            onPositiveClick: () => {
              deleteRecord(record.id);
            }
          });
        }
      }
    ]
  });

  const actionRef = ref();
  const editFlag = ref("add");

  const richTextTitle = ref("添加");
  const drawerShowFlag = ref(false);

  const drawerClosed = () => {
    reloadTable();
    drawerShowFlag.value = false;
  };

  const richText = reactive({
    id: "",
    platformCode: "",
    title: "",
    saasId: "",
    appCode: "",
    type: "",
    userClientType: "",
    terminalType: "",
    fileType: "",
    url: "",
    content: "",
  });

  const rules = computed(() => {
    const base = {
      saasId: {
        required: true,
        message: "请选择租户",
        trigger: "blur"
      },
      title: {
        required: true,
        message: "请输入标题",
        trigger: "blur"
      },
      appCode: {
        required: true,
        message: "选择渠道编码",
        trigger: "blur"
      },
      userClientType: {
        required: true,
        message: "选择用户终端",
        trigger: "blur"
      },
      terminalType: {
        required: true,
        message: "选择物理终端",
        trigger: "blur"
      },
      type: {
        required: true,
        message: "选择内容分类",
        trigger: "blur"
      },
      fileType: {
        required: true,
        message: "选择文件类型",
        trigger: "blur"
      },
    }
    if (richText.type === "VIDEO") {
      return {
        ...base,
        url: {
          required: true,
          message: "请输入视频URL",
          trigger: "blur"
        }
      }
    } else if (richText.type === "RICH_TEXT") {
      return {
        ...base,
        content: {
          required: true,
          message: "请填写内容",
          trigger: "blur"
        }
      }
    }
    return base
  });

  const params = reactive({
    platformCode: useSaas.getPlatformCode,
    saasId: "",
    type: null,
    title: "",
    userClientType: ""
  });

  const reloadTable = () => {
    actionRef.value.reload();
  };

  const resetParams = () => {
    resetObj(params, {
      saasId: params.saasId,
      type: null,
      name: null,
      createdDate: null
    });
    reloadTable();
  };

  const handleAdd = () => {
    richTextTitle.value = "添加";
    editFlag.value = "add";

    resetObj(richText);

    richText.platformCode = useSaas.getPlatformCode;
    drawerShowFlag.value = true;
  };

  const formRef = ref();
  const saveBtn = () => {
    formRef.value.validate((errors: boolean) => {
      if (!errors) {
        if (editFlag.value === "add") {
          addRecord(richText);
        } else {
          editRecord(richText);
        }
        drawerShowFlag.value = false;
      }
    });
  };

  onMounted(() => {
    params.saasId = useSaas.getSaasId;
    reloadTable();
  });
</script>

<style lang="less" scoped>
</style>
