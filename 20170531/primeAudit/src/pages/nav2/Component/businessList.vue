<!--		业务类型		-->

<template>
	<div v-if="visible">
		<div class="modal fade in" id="myModal" style="display: block; padding-right: 21px;">
	        <div class="modal-dialog">
	            <div class="modal-content">
	                <div class="modal-header">
	                    <button type="button" class="close" data-dismiss="modal" aria-hidden="true" @click="close">×</button>
	                    <h4 class="modal-title" id="myModalLabel">项目管理 > 已激活 > 新增 > 业务类型</h4>
	                </div>
	                <div class="modal-body">
	                	<div class="button-div">
	                		<div class="fuhejilu">
			                    <el-button @click="confirm" type="primary" class="btn btn-default fuheBut"><span class="fa fa-save"></span>确认</el-button>
			                    <el-button @click="close" type="primary" class="btn btn-default fuheBut"><span class="fa fa-upload"></span>取消</el-button>
		                    </div>
	                  	</div>
	                  	<div style="height:100%">
		                	<table id="customerTable" cellspacing="0" class="table table-striped" >
		                        <thead class="unitThead">
		                          <tr>
		                              <th width="30"><span class="glyphicon glyphicon-search" id="dataSearch"></span></th>
		                              <th>编号</th>
		                              <th>类型名称</th>
		                              <!--th>简称</th>
		                              <th>是否启用</th>
		                              <th>上级</th-->
		                          </tr>
		                        </thead>
		                        <tbody class="cutTaBody">
		                          <template v-for="(item,key) in businessList">
		                            <tr v-on:click="chooseList(item.Id,item.Name)" >
		                              <td>{{key+1}}</td>
		                              <td>{{item.Code}}</td>
		                              <td>{{item.Name}}</td>
		                              <!--td>{{item.ShortName}}</td>
		                              <td><span v-if="item.IsEnabled">是</span><span v-else>否</span></td>
		                              <td>{{item.ParentId.Name}}</td-->
		                            </tr>
		                          </template>

		                        </tbody>
		                    </table>
	                    </div>
	                  	<div style="clear:both"></div>
	                </div>

	            </div>
	            <!-- /.modal-content -->
	        </div>
	        <!-- /.modal-dialog -->
	    </div>
	</div>
</template>

<script>
import axios from 'axios'
import qs from 'qs'

export default{
	data() {
		return{
			businessList: [],
			businessName: "",
			businessId: ""
		}
	},
	props: {
		visible: Boolean
	},
	methods: {
		close () {
	      this.$emit('close');
	    },
	    chooseList(businessId,businessName) {
	    	this.businessId = businessId
	    	this.businessName = businessName
	    },
	    confirm() {
	    	this.$emit("businessName",this.businessName)
	    	this.$emit("businessId",this.businessId)
	    	this.$emit("close")
	   		//console.log(this.businessId)
	    }

	},
	beforeMount() {
		var self = this
	    var getCodePars = {
	    'limit':"10",
	    'page':"1",
	    'p_schema':"BusinessType/BusinessTypeSelector",
	    'start':"0",
	    'filter':"[]",
	    'isSelect':"false",
	    'sort':"[]"
	    }
	    axios.post("http://dingxin.cmsmate.cn:80/form/TreeList",
	        qs.stringify(getCodePars)
	        , {
	        headers: {'Content-Type': 'application/x-www-form-urlencoded'},
	      })
	    .then(function (response) {
//	      	console.log(response.data.data)
	      	self.businessList = JSON.parse(response.data.data)
	      	self.businessList = self.businessList.Data
	    })
	    .catch(function (error) {
	      console.log(error);
	    });
	}
}
</script>

<style scoped lang="scss">
/**	对话框样式	**/
#addModal {margin-top: 200px; }
.modal-dialog {width: 500px;}
.modal-content{}
.modal-header{background-color: #1dbba4; color:#fff;font-family:"Microsoft YaHei",Arial,Helvetica,sans-serif,"微软雅黑"; padding: 0px !important; padding-left: 10px !important;}
.modal-header button{color: red;font-size: 24px; }
.modal-title{font-weight: normal;font-size: 13px; height: 30px; line-height: 30px; }
.cusGroup{height: 36px;line-height: 36px;}
.cusConLabel{text-align: right;}
.button-div{margin-left: 10px;margin-top: 10px;margin-bottom: 10px;}
.modal{
	z-index: 1080;
}
.modal-backdrop{
	z-index: 1060;
}
.modal-body{
  max-height: 500px;
/*  overflow-y: auto;*/
  padding: 10px;
}

.modal-body label{
  font-weight: normal;
  font-size: 13px;
}

#cusTool{float:left;}
.toolSearch{margin-bottom: 0px;}
.cusAdd{background-color: #fff!important;color: #1dbba4 !important;border: 1px solid #1dbba4 !important;}
.cusAdd:hover{background-color: #1dbba4!important;color: #ffffff !important;}
.cusPus{padding-right: 6px !important;}
.clear{clear: both;}
.cusSearch input{display: block;width: 100%;height: 30px;padding: 6px 12px;font-size: 13px;line-height: 1.42857143;color: #555;background-color: #fff;background-image: none;border: 1px solid #ccc;border-radius: 4px;-webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075);box-shadow: inset 0 1px 1px rgba(0,0,0,.075);-webkit-transition: border-color ease-in-out .15s,-webkit-box-shadow ease-in-out .15s;-o-transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s;transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s;}
.cusFoot{ height: 40px;}
.cusPagNum{ text-align: right;height: 40px; line-height: 40px;
  .pagination{margin: 0px;}
}
.cusTabInfo{height: 40px;line-height: 40px;}
.table{margin-bottom: 10px; border-bottom: 1px solid #cdcece;}

.button-div{margin-left: 10px;margin-top: 10px;margin-bottom: 10px;}
/*
.fuheBut{background-color:#ffffff;color: #1dbba4;border: 1px #1dbba4 solid;}
.fuheBut:hover{background-color:#1dbba4;color: #ffffff;border: 1px #1dbba4 solid;}
*/
thead {background-color: #1dbba4}
tbody tr:hover{
  background-color: #C9E9E5;
}

.fuhejilu{
  .fuheBut{background-color:#ffffff;color: #1dbba4;border: 1px #1dbba4 solid; height: 30px; width: 60px;line-height: 5px; font-size: 13px;}
  .fuheBut:hover{background-color:#1dbba4;color: #ffffff;border: 1px #1dbba4 solid;}
}

/*	表格样式	*/
#dataSearch{padding-left:0px;}
#customerTable{margin-top: 10px !important;}
#customerTable:hover{cursor:pointer;}
#customerTable>thead{background-color: #a1d9d1;font-family:"微软雅黑","Microsoft YaHei",Arial,Helvetica,sans-serif;border-bottom: 0px;}
#customerTable>thead>tr th{font-weight: normal;font-weight: 400;height: 30px;font-size:13px;text-align: center;border-bottom: 0px solid #111;padding: 0px;line-height: 30px;}
.cutTaBody{border: 0px; }

.cutTaBody tr{height: 30px;border-right: 0px solid #cdcece;font-family:"Microsoft YaHei",Arial,Helvetica,sans-serif,"宋体";}
.cutTaBody tr:hover{background-color:#e8fffc;font-family:"Microsoft YaHei",Arial,Helvetica,sans-serif,"宋体";}
.cutTaBody tr td{text-align: center;border-right: 1px solid #cdcece;overflow:hidden;text-overflow:ellipsis;word-break:keep-all;white-space:nowrap;font-size:13px !important;font-family:"Microsoft YaHei",Arial,Helvetica,sans-serif,"宋体";height: 30px;padding:0px 8px; line-height: 30px;}
.tooltip{background-color: red!important; color: red;}
table.dataTable.no-footer {border-bottom: 1px solid #cdcece;}
.el-button{padding: 0px}
</style>