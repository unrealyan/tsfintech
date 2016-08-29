@hygotest 2016-08-29 21:58 字数 12298 阅读 0
接口文档通用参数

_pageNo: 当前页码,从0开始

_pageSize: 每页显示的数据量

List< T >：数据集

Page< T >:

    pageable：
        page:当前页码
        size:每页显示的数据量
    total：总记录数
    content：List<T>为当前页的数据集
Date: 以时间戳的方式传递

version:用于避免前端页面修改的并发冲突

资产台账接口

一丶查询三方机构信息

GET: /rest/{orgId}/OrganiztionDto/query/findOrganization

Parameters

Type	Name	Description	Required	Schema	Enums
PathParameter	orgId		true	Long	
Responses

HTTP Code	Description	Schema
200	Success	List<OrganiztionDto>
417	Validation failed	string
500	Server side error	string
二、显示资产台账

1、GET: /rest/{orgId}/AssetDetailDto/query/findAssetDetail

Parameters

Type	Name	Description	Required	Schema
QueryParameter	assetOrgIds	资产机构id,多个以“,”分割	false	String
QueryParameter	fundOrgIds	资金机构id,多个以“,”分割	false	String
QueryParameter	trustOrgIds	信托机构id,多个以“,”分割	false	String
QueryParameter	_pageNo			Integer
QueryParameter	_pageSize			Integer
Responses

HTTP Code	Description	Schema
200	Success	Page<AssetDetailDto>
417	Validation failed	string
500	Server side error	string
三、Definitions

OrganiztionDto

Name	Description	Required	Schema	Enums
orgId	机构id	true	Long	
orgType	机构类型	true	String	TRUST_ORG:信托机构
FUND_ORG:资金机构
ASSET_ORG:资产机构
orgName	机构名称	true	String	
AssetDetailDto

Name	Description	Required	Schema	Enums
loanNo	贷款业务号	true	String	
trustName	信托计划名称	true	String	
name	借款人	true	String	
idNo	身份证	true	String	
totalLoan_amount	借款金额	true	String	
productName	产品	true	String	
loanStatus	状态	true	String	
assetList	资产质量	true	List<AssetDetail>	
tenor	借款期限	true	String	
loanInterest_rate	贷款利率	true	String	
city	城市	true	String	
loanStartDate	放款日期	true	Date	
loanEndDate	到期日期	true	Date	
leftAmount	贷款余额	true	String	
AssetDetail

Name	Description	Required	Schema	Enums
period	期次	true	Integer	
status	状态		String	0:未到, 1:没有, 2:正常, 3:逾期未还, 4:逾期还清, 5:提前还款
duration	天数	true	Integer	
项目进度接口

一丶适用于项目列表中项目进度查询

GET: /rest/{orgId}/ProjectProgressDto/query/findProjectProgress

Parameters

Type	Name	Description	Required	Schema
PathParameter	orgId		true	Long
QueryParameter	_pageNo		true	Integer
QueryParameter	_pageSize		true	Integer
Responses

HTTP Code	Description	Schema
200	Success	Page< ProjectProgressDto >
417	Validation failed	string
500	Server side error	string
二、适用于查询某一个信托计划及它的项目进度

PUT: /rest/{orgId}/ProjectProgressDto/{id}

Parameters

Type	Name	Description	Required	Schema
PathParameter	orgId		true	Long
PathParameter	id		true	Long
Responses

HTTP Code	Description	Schema
200	Success	ProjectProgressDto
417	Validation failed	string
500	Server side error	string
三、适用于用户更新某个信托计划的项目进度

PUT: /rest/{orgId}/ProjectProgress/{id}

Parameters

Type	Name	Description	Required	Schema
PathParameter	orgId		true	Long
PathParameter	id		true	Long
BodyParameter			true	ProjectProgress
Responses

HTTP Code	Description	Schema
200	Success	string
417	Validation failed	string
500	Server side error	string
四、适用于用户新增某个信托计划的项目进度

POST: /rest/{orgId}/ProjectProgress

Parameters

Type	Name	Description	Required	Schema
PathParameter	orgId		true	Long
BodyParameter			true	ProjectProgress
Responses

HTTP Code	Description	Schema
200	Success	ProjectProgress
417	Validation failed	string
500	Server side error	string
五、适用于用户删除某个信托计划的项目进度

DELETE: /rest/{orgId}/ProjectProgress/{id}

Parameters

Type	Name	Description	Required	Schema
PathParameter	orgId		true	Long
PathParameter	id		true	Long
Responses

HTTP Code	Description	Schema
200	Success	ProjectProgress
417	Validation failed	string
500	Server side error	string
Definitions

ProjectProgressDto

Name	Description	Required	Schema
id		true	long
version	版本	true	Integer
trustNo	信托项目编号	true	String
orgName	信托机构	true	String
trustName	信托计划名字	true	String
trustType	项目类型	true	String
createdTime	起始日期	true	Date
trustPeriod	信托期次	true	String
fundAmount	资金规模	true	String
projectProgressList	项目进度集合	true	List<ProjectProgress>
ProjectProgress

Name	Description	Required	Schema	Enums
id		true	Long	
version	版本	true	Integer	
name	进度名字	true	String	
dateProgress	进度日期	true	Date	
complete	进度状态	true	boolean	
trustPlanId	信托计划Id	true	Long	
还款查询接口

一、适用于查询三方机构信息

GET: /rest/{orgId}/OrganiztionDto/query/findOrganization

Parameters

Type	Name	Description	Required	Schema	Enums
PathParameter	orgId		true	Long	
Responses

HTTP Code	Description	Schema
200	Success	List< OrganiztionDto >
417	Validation failed	string
500	Server side error	string
二、适用于查询所有的还款信息

GET: /rest/{orgId}/RepaymentDto/query/findRepayment

Parameters

Type	Name	Description	Required	Schema
PathParameter	orgId		true	Long
QueryParameter	assetOrgIds	资产机构id,多个以“,”分割	false	String
QueryParameter	fundOrgIds	资金机构id,多个以“,”分割	false	String
QueryParameter	trustOrgIds	信托机构id,多个以“,”分割	false	String
QueryParameter	_pageNo			Integer
QueryParameter	_pageSize			Integer
Responses

HTTP Code	Description	Schema
200	Success	Page< RepaymentDto >
417	Validation failed	string
500	Server side error	string
三、适用于查询某个还款信息的详情信息

GET: /rest/{orgId}/RepaymentDto/{id}

Parameters

Type	Name	Description	Required	Schema
PathParameter	orgId		true	Long
PathParameter	id		true	Long
Responses

HTTP Code	Description	Schema
200	Success	RepaymentDto
417	Validation failed	string
500	Server side error	string
四、Definitions

OrganiztionDto

Name	Description	Required	Schema	Enums
orgId	机构id	true	Long	
orgType	机构类型	true	String	TRUST_ORG:信托机构
FUND_ORG:资金机构
ASSET_ORG:资产机构
orgName	机构名称	true	String	
RepaymentDto

Name	Description	Required	Schema	Enums
id		true	Long	
loanNo	贷款业务号	true	String	
repaymentTransNo	还款业务流水	true	String	
bankTransNo	银行交易流水	true	String	
repaymentDate	还款日期	true	String	
totalRepaymentAmount	还款总金额	true	BigDecimal	
normalPrincipleRepayment	归还正常本金金额	true	BigDecimal	
overduePrincipleRepayment	归还逾期本金金额	true	BigDecimal	
overduePrinciplePenaltyInterestPayment	归还逾期本金罚息金额	true	BigDecimal	
normalInterestPayment	归还正常利息金额	true	BigDecimal	
overdueInterestPayment	归还逾期利息金额	true	BigDecimal	
overdueInterestPenaltyInterestPayment	归还逾期利息罚息金额	true	BigDecimal	
repaymentType	还款类型	true	String	1-正常收回 2-担保人代还 3-以资抵债 4-提前还款[部分] 5-提前还款[全部] 6-提前还款[部分]非线上 7-提前还款[全部]非线上 8-正常收回非线上 9-逾期还款 10-逾期还款非线上 100-其他
name	姓名	true	String	
idNo	证件号码	true	String	
mobilePhoneNo	手机号码	true	String	
productName	产品名称	true	String	
totalLoanAmount	贷款总额	true	BigDecimal	
放款信息筛选接口

一、适用于显示筛选信息

GET: /rest/{orgId}/LoanInformationDto/query/findLoanInformation

Parameters

Type	Name	Description	Required	Schema
PathParameter	orgId		true	Long
Responses

HTTP Code	Description	Schema
200	Success	LoanInformationDto
417	Validation failed	string
500	Server side error	string
二、适用于放款信息筛选查询

GET: /rest/{orgId}/LoanInfoDto/query/findLoanInfo

Parameters

Type	Name	Description	Required	Schema	Enums
PathParameter	orgId		true	Long	
QueryParameter	_pageNo		true	Integer	
QueryParameter	_pageSize		true	Integer	
QueryParameter	loanNo		false	String	
QueryParameter	orgName	信托公司	false	String	
QueryParameter	trustName	信托计划	false	String	
QueryParameter	productName	产品名称	false	String	
QueryParameter	loanStatus	贷款状态	false	String	APPLY: 收到申请 TS_VALID: 全思校验通过 TS_INVALID: 全思校验不通过 INVALID: 信托审批不通 VALID: 信托审批通过 LOAN_SUCCESS: 放款成功 LOAN_FAILED: 放款失败
QueryParameter	repaymentMethod	还款方式	false	String	10:按月等额本息 20:按月等额本金 30:按月还息到期还本 40:按季还息到期还本 50:到期一次性还本付息 60:自定义还款 70:其他
QueryParameter	minAmount	最小资金	false	BigDecimal	
QueryParameter	maxAmount	最大资金	false	BigDecimal	
QueryParameter	startDate	开始日期	false	Date	
QueryParameter	EndDate	结束日期	false	Date	
Responses

HTTP Code	Description	Schema
200	Success	Page< LoanInfoDto >
417	Validation failed	string
500	Server side error	string
Definitions

LoanInformationDto

Name	Description	Required	Schema
orgNames	信托公司名称集合	true	List< String >
trustNames	信托计划名称集合	true	List< String >
productNames	产品名称集合	true	List< String >
fundRanges	资金范围信息	true	List<FundRangeDto>
FundRangeDto

Name	Description	Required	Schema
fundMax	最大资金	true	BigDecimal
fundMin	最小资金	true	BigDecimal
fundCount	资金范围中的数量	true	int
LoanInfoDto

Name	Description	Required	Schema	Enums
id		true	Long	
loanNo	贷款业务号	true	String	
loanContractNo	贷款合同号	true	String	
productName	产品名称	true	String	
productType	业务种类细分	true	String	
repaymentMethod	还款方式	true	String	
repaymentFrequency	还款频率	true	String	
currency	币种	true	String	
totalLoanAmount	贷款总额	true	String	
loanInterestRate	贷款利率	true	String	
penaltyInterestRatePerDay	罚息日利息	true	String	
tenor	期限	true	String	
startDate	开始日期	true	Date	
endDate	结束日期	true	Date	
loanStartDate	贷款开始日期（贷款起息日）	true	Date	
loanEndDate	贷款结束日期(应还款日期)	true	Date	
applicationDate	申请日期	true	Date	
name	姓名	true	String	
idType	证件类型	true	String	0-身份证 1-户口簿 2-护照 3-军官证 4-士兵证 5-港澳居民来往内地通行证 6-台湾同胞来往内地通行证 7-临时身份证 8-外国人居留证 9-警官证 A-香港身份证 B-澳门身份证 C-台湾身份证 X-其他证件
idNo	证件号码	true	String	
mobilePhoneNo	手机号码	true	String	
loanStatus	贷款状态	true	String	APPLY: 收到申请 TS_VALID: 全思校验成功 TS_INVALID: 全思校验失败 INVALID: 信托审批不通过 VALID: 信托审批通过 LOAN_SUCCESS: 放款成功 LOAN_FAILED: 放款失败
尽职调查接口

一丶查询客户档案

GET: /rest/{orgId}/DueDiligence/query/findDueDiligenceInfo

Parameters

Type	Name	Description	Required	Schema	Enums
PathParameter	orgId		true	Long	
Responses

HTTP Code	Description	Schema
200	Success	List<DueDiligence>
417	Validation failed	string
500	Server side error	string
二丶增加客户档案

POST: /rest/{orgId}/DueDiligence/

Parameters

Type	Name	Description	Required	Schema	Enums
PathParameter	orgId		true	Long	
BodyParameter	itemContent		false	String	
BodyParameter	filePath		false	String	
Responses

HTTP Code	Description	Schema
200	Success	id
417	Validation failed	string
500	Server side error	string
三丶修改客户档案

PUT: /rest/{orgId}/DueDiligence/{id}

Parameters

Type	Name	Description	Required	Schema	Enums
PathParameter	orgId		true	Long	
BodyParameter	id		true	Long	
BodyParameter	itemContent		false	String	
BodyParameter	filePath		false	String	
Responses

HTTP Code	Description	Schema
200	Success	id
417	Validation failed	string
500	Server side error	string
四丶删除客户档案

DELETE: /rest/{orgId}/DueDiligence/{id}

Parameters

Type	Name	Description	Required	Schema
BodyParameter	orgId		true	Long
BodyParameter	id		true	Long
BodyParameter	filePath		true	String
Responses

HTTP Code	Description	Schema
200	Success	id
417	Validation failed	string
500	Server side error	string
五、Definitions

DueDiligence

Name	Description	Required	Schema	Enum
itemType		true	String	BASIC_INFORMATION:基本信息 COMPANY_PROFILEe:公司介绍 PRODUCT_DESCRIPTION:产品介绍 LOAN_MANAGEMENT_PROCESS :贷款管理流程 STOCK_ASSETS:存量资产 FINANCIAL_SITUATION :财务情况 IT_SYSTEMS:IT系统 DATA_SYSTEMS:数据系统 RISK_APPETITE:风险偏好
itemContent	文本内容	false	String	
filePath	附件:oss地址	false	String	
version	版本号	true	Integer	
通知中心

一丶查询信息中心

GET: /rest/{orgId}/MessageCenter/query/findMessages

Parameters

Type	Name	Description	Required	Schema	Enums
PathParameter	orgId		true	Long	
Responses

HTTP Code	Description	Schema
200	Success	List<MessageCenter>
417	Validation failed	string
500	Server side error	string
二丶更改信息处理状态

PUT: /rest/{orgId}/MessageCenter/{id}

Parameters

Type	Name	Description	Required	Schema	Enums
PathParameter	orgId		true	Long	
PathParameter	id		true	Long	
BodyParameter	status		true	String	
Responses

HTTP Code	Description	Schema
200	Success	id
417	Validation failed	string
500	Server side error	string
三丶查询信息详情

GET: /rest/{orgId}/MessageCenter/findMessageDetail/{id}

Parameters

Type	Name	Description	Required	Schema	Enums
BodyParameter	orgId		true	Long	
BodyParameter	id		true	Long	
Responses

HTTP Code	Description	Schema
200	Success	Message
417	Validation failed	string
500	Server side error	string
三、Definitions

MessageCenter

Name	Description	Required	Schema	Enum
id		true	Long	
messageType	信息类型	true	Long	0:项目评估 1:资产分析 2:企业资料 3:新增放款 4:放款失败 5:新增逾期
messageContent	信息内容		String	
createTime	时间	true	Date	
status	状态			0:未读 1:已读
version	版本号	true	Integer	
Message

Name	Description	Required	Schema	Enum
id		true	Long	
messageType	信息类型	true	Long	0:项目评估 1:资产分析 2:企业资料 3:新增放款 4:放款失败 5:新增逾期
messageContent	信息内容	true	String	
createTime	时间	true	Date	
status	状态	true	Long	0:未读 1:已读
还款信息筛选

一、查询产品名称、信托项目名称(下拉菜单)

GET: /rest/{orgId}/RepaymentDto/query/findRepaymentFilter

Parameters

Type	Name	Description	Required	Schema	Enum
PathParameter	orgId	机构id	true	Long	
Responses

HTTP Code	Description	Schema
200	Success	RepaymentInfoDto
417	Validation failed	string
500	Server side error	string
二、根据当前用户机构id查询相应信托计划下面资金规模和可放放款金额

GET: /rest/{orgId}/RepaymentDto/query/findRepayment

Parameters

Type	Name	Description	Required	Schema	Enum
PathParameter	orgId	机构id	true	Long	
BodyParameter	loanNo	业务流水号	true	Long	
BodyParameter	date	时间	true	Date	
BodyParameter	idNo	身份证号码	true	Long	
BodyParameter	name	姓名	true	Sting	
BodyParameter	productName	产品名称	true	Sting	1-正常收回;2-担保人代还;3-以资抵债；4-提前还款（部分）;5-提前还款（全部）;6-提前还款（部分）非线上；7-提前还款（全部）非线上;8-正常收回非线上；9-逾期还款;10-逾期还款非线上;11-减免;100-其他;
BodyParameter	trustName	信托项目	true	Sting	
BodyParameter	repaymetType	还款类型	true	Sting	
BodyParameter	repaymentMinAmount	还款最小金额	true	BigDecimal	
BodyParameter	repaymentMaxAmount	还款最大金额	true	BigDecimal	
Responses

HTTP Code	Description	Schema
200	Success	List<RepaymentDto>
417	Validation failed	string
500	Server side error	string
Definitions

RepaymentRangeAmountDto

Name	Description	Required	Schema
repaymentMinAmount	还款最小金额	true	BigDecimal
repaymentMaxAmount	还款最大金额	true	BigDecimal
amount	区间范围内还款笔数	true	int
RepaymentDto

Name	Description	Required	Schema
loanNo	还款业务号		
name	姓名		
idNo	身份证		
mobelNo	手机号码		
totalAmount	贷款金额		
productName	产品名称		
repaymentType	还款类型		
RepaymentInfoDto

Name	Description	Required	Schema
productName	产品名称	true	
trustName	信托项目	true	
项目关系图

一、根据当前用户机构id查询资金与机构

GET: /rest/{orgId}/OrgRelationShipDto/query/findOrgRelationShipList

Parameters

Type	Name	Description	Required	Schema
PathParameter	orgId	机构id	true	Long
Responses

HTTP Code	Description	Schema
200	Success	List<OrgRelationShipDto>
417	Validation failed	string
500	Server side error	string
Definitions

OrgRelationShipDto

Name	Description	Required	Schema
sourceName	起点（资产/信托）		
sourceId	起点（资产/信托 ID）		
targetName	终点（信托/资金）		
targetId	终点（信托/资金 ID）		
value	贷款余额		
账户余额查询

一、根据当前用户机构id查询相应信托计划下面资金规模和可放放款金额

GET: /rest/{orgId}/AccountBalanceDto/query/findAccountBalance

Parameters

Type	Name	Description	Required	Schema
PathParameter	orgId	机构id	true	Long
Responses

HTTP Code	Description	Schema
200	Success	List< AccountBalanceDto >
417	Validation failed	string
500	Server side error	string
Definitions

AccountBalanceDto

Name	Description	Required	Schema
trustNo	信托计划编号	true	String
trustName	信托计划名称	true	String
amount	资金规模	true	String
balance	资金余额	true	String
+
@hygotest 2016-08-29 21:58 字数 12298 阅读 0
本地文稿已同步至最新状态。
