# ions_zhiliao
ions for zhiliao


# 涉及：
## 1.登录、登出
## 2.验证码
## 3.用户管理
## 4.消息管理
## 5.RBAC权限管理，可配置角色，权限，用户等
## 6.echarts图表
## 7.excl文件数据导入数据库
## 8.分页，多条删除等增删改查
## 9.车辆管理等流程审核
## 10.财务中心，个人中心等信息查询及导入

#启动流程
#项目依赖
```go
go mod tidy
```
##创建数据库
手动迁移数据库或者sql强插
```go
go run main.go orm
2021/10/05 18:51:20.438 [I] [proc.go:6315]  host:localhost|port:3306|db:ions_zhiliao
orm command usage:

    syncdb     - auto create tables
    sqlall     - print sql of create tables
    help       - print this help

exit status 2
```
> syncdb 迁移数据结构到数据库；数据创建表结构语句但是不创建表
```bigquery

/*
 
SET FOREIGN_KEY_CHECKS=0;

-- ----------------------------
-- Table structure for sys_auth
-- ----------------------------
DROP TABLE IF EXISTS `sys_auth`;
CREATE TABLE `sys_auth` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `auth_name` varchar(64) NOT NULL DEFAULT '' COMMENT '权限名称',
  `url_for` varchar(255) NOT NULL DEFAULT '' COMMENT 'url反转',
  `pid` int(11) NOT NULL DEFAULT '0' COMMENT '父节点id',
  `desc` varchar(255) NOT NULL DEFAULT '' COMMENT '描述',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  `is_active` int(11) NOT NULL DEFAULT '0' COMMENT '1启用，0停用',
  `is_delete` int(11) NOT NULL DEFAULT '0' COMMENT '1删除，0未删除',
  `weight` int(11) NOT NULL DEFAULT '0' COMMENT '权重，数值越大，权重越大',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=69 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_auth
-- ----------------------------
INSERT INTO `sys_auth` VALUES ('2', '用户管理', '#', '0', '用户管理，一级菜单', '2020-08-04 15:29:05', '1', '0', '100');
INSERT INTO `sys_auth` VALUES ('3', '用户列表', 'UserController.List', '2', '用户列表,二级菜单', '2020-08-04 15:34:32', '1', '0', '99');
INSERT INTO `sys_auth` VALUES ('4', '权限管理', '#', '0', '权限管理，一级菜单', '2020-08-04 15:36:26', '1', '0', '1');
INSERT INTO `sys_auth` VALUES ('41', '权限列表', 'AuthController.List', '4', '权限列表,二级菜单', '2020-08-05 09:38:42', '1', '0', '97');
INSERT INTO `sys_auth` VALUES ('45', '角色列表', 'RoleController.List', '4', '角色列表,二级菜单', '2020-08-05 13:37:45', '1', '0', '96');
INSERT INTO `sys_auth` VALUES ('46', '个人中心', '#', '0', '个人中心，一级菜单', '2020-08-10 09:53:04', '1', '0', '95');
INSERT INTO `sys_auth` VALUES ('47', '个人信息', 'MyCenterController.Get', '46', '个人信息，二级菜单', '2020-08-10 09:53:59', '1', '0', '94');
INSERT INTO `sys_auth` VALUES ('48', '工资条', 'SalarySlipController.Get', '46', '工资条，二级菜单', '2020-08-10 09:54:28', '1', '0', '93');
INSERT INTO `sys_auth` VALUES ('49', '财务中心', '#', '0', '财务中心，一级菜单', '2020-08-10 14:47:26', '1', '0', '92');
INSERT INTO `sys_auth` VALUES ('50', '工资条', 'CaiWuSalarySlipController.Get', '49', '工资条', '2020-08-10 14:47:53', '1', '0', '91');
INSERT INTO `sys_auth` VALUES ('51', '财务报表', 'CaiWuEchartDataController.Get', '49', '财务报表，二级菜单', '2020-08-11 09:58:01', '1', '0', '90');
INSERT INTO `sys_auth` VALUES ('52', '内容管理', '#', '0', '内容管理，一级菜单', '2020-08-11 11:40:08', '1', '0', '89');
INSERT INTO `sys_auth` VALUES ('53', '栏目列表', 'CategoryController.Get', '52', '栏目管理，二级菜单', '2020-08-11 11:40:32', '1', '0', '88');
INSERT INTO `sys_auth` VALUES ('54', '新闻列表', 'NewsController.Get', '52', '新闻列表，二级菜单', '2020-08-11 11:40:56', '1', '0', '87');
INSERT INTO `sys_auth` VALUES ('55', '车辆管理', '#', '0', '车辆管理，一级菜单', '2020-08-12 13:32:54', '1', '0', '86');
INSERT INTO `sys_auth` VALUES ('56', '车辆品牌管理', 'CarBrandController.Get', '55', '车辆品牌管理，二级菜单', '2020-08-12 13:33:34', '1', '0', '85');
INSERT INTO `sys_auth` VALUES ('57', '车辆列表', 'CarsController.Get', '55', '车辆列表，二级菜单', '2020-08-12 13:34:04', '1', '0', '84');
INSERT INTO `sys_auth` VALUES ('58', '车辆申请', 'CarsApplyController.Get', '55', '车辆申请，二级菜单', '2020-08-12 13:34:34', '1', '0', '83');
INSERT INTO `sys_auth` VALUES ('59', '车辆审批', 'CarsApplyController.AuditApply', '55', '车辆审批，二级菜单', '2020-08-12 13:34:58', '1', '0', '81');
INSERT INTO `sys_auth` VALUES ('60', '我的申请', 'CarsApplyController.MyApply', '55', '我的申请。二级菜单', '2020-08-13 09:43:42', '1', '0', '82');
INSERT INTO `sys_auth` VALUES ('63', '报表管理', '#', '0', '报表管理，一级菜单', '2020-08-13 15:51:33', '1', '0', '81');
INSERT INTO `sys_auth` VALUES ('64', '财务报表', 'EchartsCaiwuController.Get', '63', '财务报表，二级菜单', '2020-08-13 15:52:11', '1', '0', '80');
INSERT INTO `sys_auth` VALUES ('65', '业务报表', 'EchartsBusinessController.Get', '63', '业务报表，二级菜单', '2020-08-13 15:52:38', '1', '0', '79');
INSERT INTO `sys_auth` VALUES ('66', '课程报表', 'EchartsCourseController.Get', '63', '课程报表，二级菜单', '2020-08-13 15:53:03', '1', '0', '78');
INSERT INTO `sys_auth` VALUES ('67', '测试', '#', '0', '测试,一级菜单', '2020-08-18 14:26:44', '1', '0', '9999');
INSERT INTO `sys_auth` VALUES ('68', '测试2', '#', '0', '测试2', '2020-08-18 14:27:42', '1', '0', '1');

-- ----------------------------
-- Table structure for sys_caiwu_data
-- ----------------------------
DROP TABLE IF EXISTS `sys_caiwu_data`;
CREATE TABLE `sys_caiwu_data` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `caiwu_date` varchar(32) NOT NULL DEFAULT '' COMMENT '财务月份',
  `sales_volume` decimal(10,2) NOT NULL DEFAULT '0.00' COMMENT '本月销售额',
  `student_incress` int(11) NOT NULL DEFAULT '0' COMMENT '学员增加数',
  `django` int(11) NOT NULL DEFAULT '0' COMMENT 'django课程卖出数量',
  `vue_django` int(11) NOT NULL DEFAULT '0' COMMENT 'vue+django课程卖出数量',
  `celery` int(11) NOT NULL DEFAULT '0' COMMENT 'celery课程卖出数量',
  `create_date` datetime NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=10 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_caiwu_data
-- ----------------------------
INSERT INTO `sys_caiwu_data` VALUES ('7', '2020-08', '5.00', '200', '50', '30', '10', '2020-08-11 10:59:06');
INSERT INTO `sys_caiwu_data` VALUES ('8', '2020-09', '8.00', '300', '80', '35', '20', '2020-08-11 10:59:06');
INSERT INTO `sys_caiwu_data` VALUES ('9', '2020-10', '6.00', '310', '180', '135', '20', '2020-08-11 10:59:06');

-- ----------------------------
-- Table structure for sys_cars
-- ----------------------------
DROP TABLE IF EXISTS `sys_cars`;
CREATE TABLE `sys_cars` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(64) NOT NULL DEFAULT '' COMMENT '车辆名称',
  `car_brand_id` int(11) NOT NULL COMMENT '车辆品牌外键',
  `status` int(11) NOT NULL DEFAULT '1' COMMENT '1:可借,2:不可借',
  `is_active` int(11) NOT NULL DEFAULT '1' COMMENT '启用:1,停用:0',
  `is_delete` int(11) NOT NULL DEFAULT '0' COMMENT '删除:1,未删除:0',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_cars
-- ----------------------------
INSERT INTO `sys_cars` VALUES ('3', '宝马x5', '3', '1', '1', '0', '2020-08-12 15:29:19');
INSERT INTO `sys_cars` VALUES ('4', '奔驰大G', '4', '2', '1', '0', '2020-08-12 15:29:32');

-- ----------------------------
-- Table structure for sys_cars_apply
-- ----------------------------
DROP TABLE IF EXISTS `sys_cars_apply`;
CREATE TABLE `sys_cars_apply` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL,
  `cars_id` int(11) NOT NULL,
  `reason` varchar(255) NOT NULL DEFAULT '' COMMENT '申请理由',
  `destination` varchar(64) NOT NULL DEFAULT '' COMMENT '目的地',
  `return_date` date NOT NULL COMMENT '归还日期',
  `return_status` int(11) NOT NULL DEFAULT '0',
  `audit_status` int(11) NOT NULL DEFAULT '3' COMMENT '1:同意，2:未同意，3:未审批',
  `audit_option` varchar(255) NOT NULL DEFAULT '' COMMENT '审批意见',
  `is_active` int(11) NOT NULL DEFAULT '1' COMMENT '启用:1,停用:0',
  `is_delete` int(11) NOT NULL DEFAULT '0' COMMENT '删除:1,未删除:0',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  `notify_tag` int(11) NOT NULL DEFAULT '0' COMMENT '1:已发送通知，0：未发送通知',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_cars_apply
-- ----------------------------
INSERT INTO `sys_cars_apply` VALUES ('4', '2', '3', 'xx', 'qq', '2020-08-18', '0', '1', '同意', '1', '0', '2020-08-18 14:09:06', '1');
INSERT INTO `sys_cars_apply` VALUES ('5', '2', '3', 'xx', 'xx', '2020-08-21', '1', '1', '同意', '1', '0', '2020-08-18 14:23:19', '0');

-- ----------------------------
-- Table structure for sys_cars_apply_copy
-- ----------------------------
DROP TABLE IF EXISTS `sys_cars_apply_copy`;
CREATE TABLE `sys_cars_apply_copy` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL,
  `cars_id` int(11) NOT NULL,
  `reason` varchar(255) NOT NULL DEFAULT '' COMMENT '申请理由',
  `destination` varchar(64) NOT NULL DEFAULT '' COMMENT '目的地',
  `return_date` date NOT NULL COMMENT '归还日期',
  `return_status` int(11) NOT NULL DEFAULT '0',
  `audit_status` int(11) NOT NULL DEFAULT '3' COMMENT '1:同意，2:未同意，3:未审批',
  `audit_option` varchar(255) NOT NULL DEFAULT '' COMMENT '审批意见',
  `is_active` int(11) NOT NULL DEFAULT '1' COMMENT '启用:1,停用:0',
  `is_delete` int(11) NOT NULL DEFAULT '0' COMMENT '删除:1,未删除:0',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_cars_apply_copy
-- ----------------------------
INSERT INTO `sys_cars_apply_copy` VALUES ('4', '2', '3', 'xx', 'qq', '2020-08-12', '0', '1', '同意', '1', '0', '2020-08-13 10:50:04');

-- ----------------------------
-- Table structure for sys_cars_brand
-- ----------------------------
DROP TABLE IF EXISTS `sys_cars_brand`;
CREATE TABLE `sys_cars_brand` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(64) NOT NULL DEFAULT '' COMMENT '品牌名称',
  `desc` varchar(255) NOT NULL DEFAULT '' COMMENT '品牌描述',
  `is_active` int(11) NOT NULL DEFAULT '1' COMMENT '启用:1,停用:0',
  `is_delete` int(11) NOT NULL DEFAULT '0' COMMENT '删除:1,未删除:0',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_cars_brand
-- ----------------------------
INSERT INTO `sys_cars_brand` VALUES ('3', '宝马', '宝马品牌', '1', '0', '2020-08-12 14:33:03');
INSERT INTO `sys_cars_brand` VALUES ('4', '奔驰', '奔驰品牌', '1', '0', '2020-08-12 14:33:29');

-- ----------------------------
-- Table structure for sys_category
-- ----------------------------
DROP TABLE IF EXISTS `sys_category`;
CREATE TABLE `sys_category` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(64) NOT NULL DEFAULT '' COMMENT '分类名称',
  `desc` varchar(255) NOT NULL DEFAULT '' COMMENT '描述',
  `is_active` int(11) NOT NULL DEFAULT '1' COMMENT '启用:1,停用:0',
  `is_delete` int(11) NOT NULL DEFAULT '0' COMMENT '删除:1,未删除:0',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_category
-- ----------------------------
INSERT INTO `sys_category` VALUES ('2', '人事', '人事栏目', '1', '0', '2020-08-11 13:53:58');
INSERT INTO `sys_category` VALUES ('3', '财务', '财务栏目', '1', '0', '2020-08-11 13:55:01');
INSERT INTO `sys_category` VALUES ('4', '市场部', '市场部', '1', '0', '2020-08-18 14:20:01');

-- ----------------------------
-- Table structure for sys_message_notify
-- ----------------------------
DROP TABLE IF EXISTS `sys_message_notify`;
CREATE TABLE `sys_message_notify` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `flag` int(11) NOT NULL DEFAULT '1' COMMENT '1:车辆逾期，2:所有通知',
  `title` varchar(64) NOT NULL DEFAULT '' COMMENT '消息标题',
  `content` longtext NOT NULL COMMENT '消息内容',
  `user_id` int(11) NOT NULL,
  `read_tag` int(11) NOT NULL DEFAULT '0' COMMENT '1:已读，0:未读',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=14 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_message_notify
-- ----------------------------
INSERT INTO `sys_message_notify` VALUES ('10', '1', '车辆归还逾期', 'admin1用户，你借的车辆归还时间为2020-08-12,已经预期，请尽快归还!!', '2', '1');
INSERT INTO `sys_message_notify` VALUES ('11', '1', '车辆归还逾期', 'admin1用户，你借的车辆归还时间为2020-08-12,已经预期，请尽快归还!!', '2', '1');
INSERT INTO `sys_message_notify` VALUES ('12', '1', '车辆归还逾期', 'admin1用户，你借的车辆归还时间为2020-08-13,已经预期，请尽快归还!!', '2', '1');
INSERT INTO `sys_message_notify` VALUES ('13', '1', '车辆归还逾期', 'admin1用户，你借的车辆归还时间为2020-08-18,已经预期，请尽快归还!!', '2', '1');

-- ----------------------------
-- Table structure for sys_news
-- ----------------------------
DROP TABLE IF EXISTS `sys_news`;
CREATE TABLE `sys_news` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `title` varchar(64) NOT NULL DEFAULT '' COMMENT '新闻标题',
  `content` longtext NOT NULL COMMENT '新闻内容',
  `is_active` int(11) NOT NULL DEFAULT '1' COMMENT '启用:1,停用:0',
  `is_delete` int(11) NOT NULL DEFAULT '0' COMMENT '删除:1,未删除:0',
  `category_id` int(11) NOT NULL,
  `create_time` datetime NOT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=9 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_news
-- ----------------------------
INSERT INTO `sys_news` VALUES ('2', 'xx', '<p>qe</p><p>eq</p><p>eqw</p><p>tq</p><p>发</p><p>恶趣味</p><p>恶趣味</p>', '1', '0', '2', '2020-08-12 10:41:14');
INSERT INTO `sys_news` VALUES ('3', '请求', '<p>阿松大</p><p>dasd qe</p><p>恶气呃</p><p>eqwe</p><p>与y</p><p>545</p>', '1', '0', '3', '2020-08-12 10:42:34');
INSERT INTO `sys_news` VALUES ('4', '阿凡达', '<p>企鹅</p><p>二期</p><p>大沙达</p><p>fs</p>', '1', '0', '2', '2020-08-12 10:43:45');
INSERT INTO `sys_news` VALUES ('5', 'e\'q\'w', '<p>eqw 恶趣味</p>', '1', '0', '3', '2020-08-12 10:44:18');
INSERT INTO `sys_news` VALUES ('6', '二期', '<p>恶趣味</p><p>dasd</p><p>das&nbsp;</p><p>da&nbsp;</p><p><br></p><p><img src=\"blob:http://127.0.0.1:8080/69e58464-d039-4c67-aa90-9a95a476474b\" style=\"width: 300px;\" class=\"fr-fic fr-rounded fr-bordered fr-shadow fr-dii\"></p>', '1', '0', '3', '2020-08-12 10:45:18');
INSERT INTO `sys_news` VALUES ('7', '阿凡达', '<p>da</p><p></p><div class=\"fr-img-space-wrap\"><span class=\"fr-img-caption fr-fic fr-dib\" style=\"width: 302px;\"><span class=\"fr-img-wrap\"><img src=\"http://127.0.0.1:8080/upload/news_img/1597203718-2.jpg\" data-code=\"200\" data-msg=\"文件上传成功\"><span class=\"fr-inner\">Image Caption</span></span></span><p class=\"fr-img-space-wrap2\">&nbsp;</p></div><p></p><p><br></p><p>达到</p>', '1', '0', '3', '2020-08-12 11:10:26');
INSERT INTO `sys_news` VALUES ('8', '学学学', '<p>是下辖</p><p><img src=\"http://127.0.0.1:8080/upload/news_img/1597731682-wiki快捷键.JPG\" style=\"width: 300px;\" class=\"fr-fic fr-dib\" data-code=\"200\" data-msg=\"文件上传成功\"></p>', '1', '0', '4', '2020-08-18 14:21:26');

-- ----------------------------
-- Table structure for sys_role
-- ----------------------------
DROP TABLE IF EXISTS `sys_role`;
CREATE TABLE `sys_role` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `role_name` varchar(64) NOT NULL DEFAULT '',
  `desc` varchar(255) NOT NULL DEFAULT '',
  `is_active` int(11) NOT NULL DEFAULT '0',
  `is_delete` int(11) NOT NULL DEFAULT '0',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_role
-- ----------------------------
INSERT INTO `sys_role` VALUES ('1', '普通管理员', '普通管理员', '1', '0', '2020-08-05 13:49:04');
INSERT INTO `sys_role` VALUES ('3', '超级管理员', '超级管理员', '1', '0', '2020-08-05 14:02:45');
INSERT INTO `sys_role` VALUES ('4', 'admin3角色', 'admin3角色', '1', '0', '2020-08-18 13:50:23');

-- ----------------------------
-- Table structure for sys_role_sys_auths
-- ----------------------------
DROP TABLE IF EXISTS `sys_role_sys_auths`;
CREATE TABLE `sys_role_sys_auths` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `sys_role_id` int(11) NOT NULL,
  `sys_auth_id` int(11) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=227 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_role_sys_auths
-- ----------------------------
INSERT INTO `sys_role_sys_auths` VALUES ('26', '3', '45');
INSERT INTO `sys_role_sys_auths` VALUES ('27', '3', '41');
INSERT INTO `sys_role_sys_auths` VALUES ('28', '3', '4');
INSERT INTO `sys_role_sys_auths` VALUES ('165', '4', '60');
INSERT INTO `sys_role_sys_auths` VALUES ('166', '4', '59');
INSERT INTO `sys_role_sys_auths` VALUES ('167', '4', '58');
INSERT INTO `sys_role_sys_auths` VALUES ('168', '4', '57');
INSERT INTO `sys_role_sys_auths` VALUES ('169', '4', '56');
INSERT INTO `sys_role_sys_auths` VALUES ('170', '4', '55');
INSERT INTO `sys_role_sys_auths` VALUES ('171', '4', '48');
INSERT INTO `sys_role_sys_auths` VALUES ('172', '4', '47');
INSERT INTO `sys_role_sys_auths` VALUES ('173', '4', '46');
INSERT INTO `sys_role_sys_auths` VALUES ('174', '4', '3');
INSERT INTO `sys_role_sys_auths` VALUES ('175', '4', '2');
INSERT INTO `sys_role_sys_auths` VALUES ('201', '1', '68');
INSERT INTO `sys_role_sys_auths` VALUES ('202', '1', '67');
INSERT INTO `sys_role_sys_auths` VALUES ('203', '1', '66');
INSERT INTO `sys_role_sys_auths` VALUES ('204', '1', '65');
INSERT INTO `sys_role_sys_auths` VALUES ('205', '1', '64');
INSERT INTO `sys_role_sys_auths` VALUES ('206', '1', '63');
INSERT INTO `sys_role_sys_auths` VALUES ('207', '1', '60');
INSERT INTO `sys_role_sys_auths` VALUES ('208', '1', '59');
INSERT INTO `sys_role_sys_auths` VALUES ('209', '1', '58');
INSERT INTO `sys_role_sys_auths` VALUES ('210', '1', '57');
INSERT INTO `sys_role_sys_auths` VALUES ('211', '1', '56');
INSERT INTO `sys_role_sys_auths` VALUES ('212', '1', '55');
INSERT INTO `sys_role_sys_auths` VALUES ('213', '1', '54');
INSERT INTO `sys_role_sys_auths` VALUES ('214', '1', '53');
INSERT INTO `sys_role_sys_auths` VALUES ('215', '1', '52');
INSERT INTO `sys_role_sys_auths` VALUES ('216', '1', '51');
INSERT INTO `sys_role_sys_auths` VALUES ('217', '1', '50');
INSERT INTO `sys_role_sys_auths` VALUES ('218', '1', '49');
INSERT INTO `sys_role_sys_auths` VALUES ('219', '1', '48');
INSERT INTO `sys_role_sys_auths` VALUES ('220', '1', '47');
INSERT INTO `sys_role_sys_auths` VALUES ('221', '1', '46');
INSERT INTO `sys_role_sys_auths` VALUES ('222', '1', '45');
INSERT INTO `sys_role_sys_auths` VALUES ('223', '1', '41');
INSERT INTO `sys_role_sys_auths` VALUES ('224', '1', '4');
INSERT INTO `sys_role_sys_auths` VALUES ('225', '1', '3');
INSERT INTO `sys_role_sys_auths` VALUES ('226', '1', '2');

-- ----------------------------
-- Table structure for sys_role_sys_users
-- ----------------------------
DROP TABLE IF EXISTS `sys_role_sys_users`;
CREATE TABLE `sys_role_sys_users` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `sys_role_id` int(11) NOT NULL,
  `sys_user_id` int(11) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=34 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_role_sys_users
-- ----------------------------
INSERT INTO `sys_role_sys_users` VALUES ('25', '1', '13');
INSERT INTO `sys_role_sys_users` VALUES ('26', '1', '15');
INSERT INTO `sys_role_sys_users` VALUES ('27', '1', '10');
INSERT INTO `sys_role_sys_users` VALUES ('28', '1', '16');
INSERT INTO `sys_role_sys_users` VALUES ('29', '1', '2');
INSERT INTO `sys_role_sys_users` VALUES ('31', '3', '2');
INSERT INTO `sys_role_sys_users` VALUES ('33', '4', '7');

-- ----------------------------
-- Table structure for sys_salary_slip
-- ----------------------------
DROP TABLE IF EXISTS `sys_salary_slip`;
CREATE TABLE `sys_salary_slip` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `card_id` varchar(64) NOT NULL DEFAULT '' COMMENT '员工工号',
  `base_pay` decimal(12,2) NOT NULL DEFAULT '0.00' COMMENT '基本工资',
  `working_days` decimal(3,1) NOT NULL DEFAULT '0.0' COMMENT '工作天数',
  `days_off` decimal(3,1) NOT NULL DEFAULT '0.0' COMMENT '请假天数',
  `days_off_no` decimal(3,1) NOT NULL DEFAULT '0.0' COMMENT '调休天数',
  `reward` decimal(8,2) NOT NULL DEFAULT '0.00' COMMENT '奖金',
  `rent_subsidy` decimal(6,2) NOT NULL DEFAULT '0.00' COMMENT '租房补贴',
  `trans_subsidy` decimal(6,2) NOT NULL DEFAULT '0.00' COMMENT '交通补贴',
  `social_security` decimal(6,2) NOT NULL DEFAULT '0.00' COMMENT '社保',
  `hous_provident_fund` decimal(6,2) NOT NULL DEFAULT '0.00' COMMENT '住房公积金',
  `personal_pncome_tax` decimal(6,2) NOT NULL DEFAULT '0.00' COMMENT '个税',
  `fine` decimal(6,2) NOT NULL DEFAULT '0.00' COMMENT '罚金',
  `net_salary` decimal(10,2) NOT NULL DEFAULT '0.00' COMMENT '实发工资',
  `pay_date` varchar(32) NOT NULL DEFAULT '' COMMENT '工资月份',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=487 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_salary_slip
-- ----------------------------
INSERT INTO `sys_salary_slip` VALUES ('466', 'zl-001', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('467', 'zl-002', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('468', 'zl-003', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('469', 'zl-004', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('470', 'zl-005', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('471', 'zl-006', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('472', 'zl-007', '5000.00', '22.0', '0.0', '0.0', '800.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6633.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('473', 'zl-008', '5000.00', '17.0', '5.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('474', 'zl-009', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('475', 'zl-010', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('476', 'zl-011', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('477', 'zl-012', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('478', 'zl-014', '12000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '342.00', '0.00', '13163.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('479', 'zl-015', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('480', 'zl-016', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('481', 'zl-017', '5000.00', '22.0', '0.0', '0.0', '500.00', '200.00', '100.00', '152.00', '147.00', '212.00', '50.00', '6383.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('482', 'zl-018', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('483', 'zl-019', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('484', 'zl-020', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('485', 'zl-021', '5000.00', '22.0', '0.0', '0.0', '200.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6033.00', '2020-08', '2020-08-11 09:39:40');
INSERT INTO `sys_salary_slip` VALUES ('486', 'zl-022', '5000.00', '22.0', '0.0', '0.0', '300.00', '200.00', '100.00', '152.00', '147.00', '212.00', '0.00', '6133.00', '2020-08', '2020-08-11 09:39:40');

-- ----------------------------
-- Table structure for sys_user
-- ----------------------------
DROP TABLE IF EXISTS `sys_user`;
CREATE TABLE `sys_user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `card_id` varchar(64) DEFAULT NULL COMMENT '工号',
  `user_name` varchar(64) NOT NULL DEFAULT '' COMMENT '用户名',
  `password` varchar(32) NOT NULL DEFAULT '' COMMENT '密码',
  `age` int(11) DEFAULT NULL COMMENT '年龄',
  `gender` int(11) DEFAULT NULL COMMENT '1:男,2:女,3:未知',
  `phone` bigint(20) DEFAULT NULL COMMENT '电话号码',
  `addr` varchar(255) DEFAULT NULL COMMENT '地址',
  `is_active` int(11) NOT NULL DEFAULT '1' COMMENT '1启用，0停用',
  `is_delete` int(11) NOT NULL DEFAULT '0' COMMENT '1删除，0未删除',
  `create_time` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `user_name` (`user_name`)
) ENGINE=InnoDB AUTO_INCREMENT=20 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of sys_user
-- ----------------------------
INSERT INTO `sys_user` VALUES ('2', 'zl-001', 'admin', 'd037ac4ce6cc4fe890ff2a5c24534c97', '23', '1', '13910241567', '北京市 西城区', '1', '0', '2020-07-31 11:42:34');
INSERT INTO `sys_user` VALUES ('3', 'zl-002', 'admin2', 'e10adc3949ba59abbe56e057f20f883e', '19', '2', '13910241567', '	北京市 海淀区', '0', '1', '2020-08-01 11:42:34');
INSERT INTO `sys_user` VALUES ('7', 'zl-003', 'admin3', 'e10adc3949ba59abbe56e057f20f883e', '11', '1', '13810342534', 'xx', '0', '0', '2020-08-01 14:35:44');
INSERT INTO `sys_user` VALUES ('8', 'zl-004', 'admin4', 'd037ac4ce6cc4fe890ff2a5c24534c97', '12', '1', '13810342534', 'cs', '1', '1', '2020-08-01 14:36:33');
INSERT INTO `sys_user` VALUES ('9', 'zl-005', 'admin5', 'd037ac4ce6cc4fe890ff2a5c24534c97', '18', '2', '13810342534', '长沙', '1', '1', '2020-08-01 14:38:26');
INSERT INTO `sys_user` VALUES ('10', 'zl-006', 'admin6', 'd037ac4ce6cc4fe890ff2a5c24534c97', '15', '1', '13810342534', '长沙', '1', '0', '2020-08-01 14:41:45');
INSERT INTO `sys_user` VALUES ('11', 'zl-007', 'admin7', 'd037ac4ce6cc4fe890ff2a5c24534c97', '13', '1', '13810342534', '信息', '1', '0', '2020-08-01 14:42:56');
INSERT INTO `sys_user` VALUES ('12', 'zl-008', 'admin8', 'd037ac4ce6cc4fe890ff2a5c24534c97', '13', '1', '13810342534', 'xxs', '1', '1', '2020-08-01 14:43:21');
INSERT INTO `sys_user` VALUES ('13', 'zl-009', 'admin9', 'd037ac4ce6cc4fe890ff2a5c24534c97', '14', '1', '13810342534', 'xx', '1', '1', '2020-08-01 14:44:55');
INSERT INTO `sys_user` VALUES ('14', 'zl-010', 'admin1011', '96e79218965eb72c92a549dd5a330112', '12', '1', '13810342534', 'a', '1', '1', '2020-08-01 14:46:26');
INSERT INTO `sys_user` VALUES ('15', 'zl-011', 'zhiliao111', '7fa8282ad93047a4d6fe6111c93b308a', '12', '1', '13810342534', 'a', '1', '0', '2020-08-01 14:46:26');
INSERT INTO `sys_user` VALUES ('16', 'zl-012', 'admin1111', 'd037ac4ce6cc4fe890ff2a5c24534c97', '0', '1', '13910342513', 'xxx', '1', '0', '2020-08-04 17:25:36');
INSERT INTO `sys_user` VALUES ('18', '', 'admin1111222', 'd037ac4ce6cc4fe890ff2a5c24534c97', '11', '2', '13810392410', 'xxx', '0', '1', '2020-08-18 13:57:57');
INSERT INTO `sys_user` VALUES ('19', '', 'admin22222', 'd037ac4ce6cc4fe890ff2a5c24534c97', '12', '1', '13412345689', 'xx', '1', '0', '2020-08-18 14:13:50');

```
