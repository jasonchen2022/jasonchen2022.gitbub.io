# 新的表结构

## 1.更新
- 初始化server后先更新一下新的表结构，主要是增加了红包等功能

```bash
/*
 Navicat Premium Data Transfer

 Source Server Type    : MySQL
 Source Server Version : 50734
 Source Schema         : openIM

 Target Server Type    : MySQL
 Target Server Version : 50734
 File Encoding         : 65001

 Date: 05/03/2023 22:07:34
*/

SET NAMES utf8mb
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for app_version
-- ----------------------------
DROP TABLE IF EXISTS `app_version`;
CREATE TABLE `app_version` (
  `version` varchar(64) DEFAULT NULL,
  `type` bigint(20) NOT NULL AUTO_INCREMENT,
  `update_time` bigint(20) DEFAULT NULL,
  `force_update` tinyint(1) DEFAULT NULL,
  `file_name` longtext,
  `yaml_name` longtext,
  `update_log` longtext,
  `download_url` varchar(255) DEFAULT NULL,
  `download_ios` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`type`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for black_lists
-- ----------------------------
DROP TABLE IF EXISTS `black_lists`;
CREATE TABLE `black_lists` (
  `uid` longtext,
  `begin_disable_time` datetime(3) DEFAULT NULL,
  `end_disable_time` datetime(3) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for blacks
-- ----------------------------
DROP TABLE IF EXISTS `blacks`;
CREATE TABLE `blacks` (
  `owner_user_id` varchar(64) NOT NULL,
  `block_user_id` varchar(64) NOT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `add_source` int(11) DEFAULT NULL,
  `operator_user_id` varchar(64) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  PRIMARY KEY (`owner_user_id`,`block_user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for chat_logs
-- ----------------------------
DROP TABLE IF EXISTS `chat_logs`;
CREATE TABLE `chat_logs` (
  `server_msg_id` char(64) CHARACTER SET utf8 NOT NULL,
  `client_msg_id` char(64) CHARACTER SET utf8 DEFAULT NULL,
  `send_id` char(64) CHARACTER SET utf8 DEFAULT NULL,
  `recv_id` char(64) CHARACTER SET utf8 DEFAULT NULL,
  `sender_platform_id` int(11) DEFAULT NULL COMMENT '平台类型 1:ios 2:android 3:windows 4:osx 5:web&mini 7:linux 8:管理员',
  `sender_nick_name` varchar(255) CHARACTER SET utf8 DEFAULT NULL,
  `sender_face_url` varchar(255) CHARACTER SET utf8 DEFAULT NULL,
  `session_type` int(11) DEFAULT NULL,
  `msg_from` int(11) DEFAULT NULL,
  `content_type` int(11) DEFAULT NULL,
  `content` text,
  `status` int(11) DEFAULT NULL,
  `send_time` datetime(3) DEFAULT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `ex` varchar(1024) CHARACTER SET utf8 DEFAULT NULL,
  PRIMARY KEY (`server_msg_id`) USING BTREE,
  KEY `content_type` (`send_time`,`content_type`) USING BTREE,
  KEY `content_type_alone` (`content_type`) USING BTREE,
  KEY `sendTime` (`send_time`) USING BTREE,
  KEY `send_id` (`send_time`,`send_id`) USING BTREE,
  KEY `recv_id` (`send_time`,`recv_id`) USING BTREE,
  KEY `session_type` (`send_time`,`session_type`) USING BTREE,
  KEY `session_type_alone` (`session_type`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- ----------------------------
-- Table structure for client_init_config
-- ----------------------------
DROP TABLE IF EXISTS `client_init_config`;
CREATE TABLE `client_init_config` (
  `discover_page_url` varchar(64) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for conversations
-- ----------------------------
DROP TABLE IF EXISTS `conversations`;
CREATE TABLE `conversations` (
  `owner_user_id` char(128) NOT NULL,
  `conversation_id` char(128) NOT NULL,
  `conversation_type` int(11) DEFAULT NULL COMMENT '会话类型 1:单聊 2:群聊',
  `user_id` char(64) DEFAULT NULL,
  `group_id` char(128) DEFAULT NULL,
  `recv_msg_opt` int(11) DEFAULT NULL,
  `unread_count` int(11) DEFAULT NULL,
  `draft_text_time` bigint(20) DEFAULT NULL,
  `is_pinned` tinyint(1) DEFAULT NULL,
  `is_private_chat` tinyint(1) DEFAULT NULL,
  `burn_duration` int(11) DEFAULT '30',
  `group_at_type` int(11) DEFAULT NULL,
  `is_not_in_group` tinyint(1) DEFAULT NULL,
  `update_unread_count_time` bigint(20) DEFAULT NULL,
  `attached_info` varchar(1024) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  PRIMARY KEY (`owner_user_id`,`conversation_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for department_members
-- ----------------------------
DROP TABLE IF EXISTS `department_members`;
CREATE TABLE `department_members` (
  `user_id` varchar(64) NOT NULL,
  `department_id` varchar(64) NOT NULL,
  `order` int(11) DEFAULT NULL,
  `position` varchar(256) DEFAULT NULL,
  `leader` int(11) DEFAULT NULL,
  `status` int(11) DEFAULT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  PRIMARY KEY (`user_id`,`department_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for departments
-- ----------------------------
DROP TABLE IF EXISTS `departments`;
CREATE TABLE `departments` (
  `department_id` varchar(64) NOT NULL,
  `face_url` varchar(255) DEFAULT NULL,
  `name` varchar(256) DEFAULT NULL,
  `parent_id` varchar(64) DEFAULT NULL,
  `order` int(11) DEFAULT NULL,
  `department_type` int(11) DEFAULT NULL,
  `related_group_id` varchar(64) DEFAULT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  PRIMARY KEY (`department_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for friend_requests
-- ----------------------------
DROP TABLE IF EXISTS `friend_requests`;
CREATE TABLE `friend_requests` (
  `from_user_id` varchar(64) NOT NULL,
  `to_user_id` varchar(64) NOT NULL,
  `handle_result` int(11) DEFAULT NULL,
  `req_msg` varchar(255) DEFAULT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `handler_user_id` varchar(64) DEFAULT NULL,
  `handle_msg` varchar(255) DEFAULT NULL,
  `handle_time` datetime(3) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  PRIMARY KEY (`from_user_id`,`to_user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for friends
-- ----------------------------
DROP TABLE IF EXISTS `friends`;
CREATE TABLE `friends` (
  `owner_user_id` varchar(64) NOT NULL,
  `friend_user_id` varchar(64) NOT NULL,
  `remark` varchar(255) DEFAULT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `add_source` int(11) DEFAULT NULL,
  `operator_user_id` varchar(64) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  PRIMARY KEY (`owner_user_id`,`friend_user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for group_members
-- ----------------------------
DROP TABLE IF EXISTS `group_members`;
CREATE TABLE `group_members` (
  `group_id` varchar(64) NOT NULL,
  `user_id` varchar(64) NOT NULL,
  `nickname` varchar(255) DEFAULT NULL,
  `user_group_face_url` varchar(255) DEFAULT NULL,
  `role_level` int(11) DEFAULT NULL,
  `join_time` datetime(3) DEFAULT NULL,
  `join_source` int(11) DEFAULT NULL,
  `inviter_user_id` varchar(64) DEFAULT NULL,
  `operator_user_id` varchar(64) DEFAULT NULL,
  `mute_end_time` datetime(3) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  PRIMARY KEY (`group_id`,`user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for group_requests
-- ----------------------------
DROP TABLE IF EXISTS `group_requests`;
CREATE TABLE `group_requests` (
  `user_id` varchar(64) NOT NULL,
  `group_id` varchar(64) NOT NULL,
  `handle_result` int(11) DEFAULT NULL,
  `req_msg` varchar(1024) DEFAULT NULL,
  `handle_msg` varchar(1024) DEFAULT NULL,
  `req_time` datetime(3) DEFAULT NULL,
  `handle_user_id` varchar(64) DEFAULT NULL,
  `handle_time` datetime(3) DEFAULT NULL,
  `join_source` int(11) DEFAULT NULL,
  `inviter_user_id` varchar(64) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  PRIMARY KEY (`user_id`,`group_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for groups
-- ----------------------------
DROP TABLE IF EXISTS `groups`;
CREATE TABLE `groups` (
  `group_id` varchar(64) NOT NULL,
  `name` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL,
  `notification` varchar(255) DEFAULT NULL,
  `introduction` varchar(255) DEFAULT NULL,
  `face_url` varchar(255) DEFAULT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `ex` longtext,
  `status` int(11) DEFAULT NULL,
  `creator_user_id` varchar(64) DEFAULT NULL,
  `group_type` int(11) DEFAULT NULL,
  `need_verification` int(11) DEFAULT NULL,
  `look_member_info` int(11) DEFAULT NULL,
  `apply_member_friend` int(11) DEFAULT NULL,
  `notification_update_time` datetime(3) DEFAULT NULL,
  `notification_user_id` varchar(64) DEFAULT NULL,
  PRIMARY KEY (`group_id`) USING BTREE,
  KEY `create_time` (`create_time`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for invitations
-- ----------------------------
DROP TABLE IF EXISTS `invitations`;
CREATE TABLE `invitations` (
  `invitation_code` varchar(32) NOT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `user_id` varchar(191) DEFAULT NULL,
  `last_time` datetime(3) DEFAULT NULL,
  `status` int(11) DEFAULT NULL,
  PRIMARY KEY (`invitation_code`) USING BTREE,
  KEY `userID` (`user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for ip_limits
-- ----------------------------
DROP TABLE IF EXISTS `ip_limits`;
CREATE TABLE `ip_limits` (
  `ip` varchar(15) NOT NULL,
  `limit_register` tinyint(4) DEFAULT NULL,
  `limit_login` tinyint(4) DEFAULT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `limit_time` datetime(3) DEFAULT NULL,
  PRIMARY KEY (`ip`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for organization_users
-- ----------------------------
DROP TABLE IF EXISTS `organization_users`;
CREATE TABLE `organization_users` (
  `user_id` varchar(64) NOT NULL,
  `nickname` varchar(256) DEFAULT NULL,
  `english_name` varchar(256) DEFAULT NULL,
  `face_url` varchar(256) DEFAULT NULL,
  `gender` int(11) DEFAULT NULL,
  `mobile` varchar(32) DEFAULT NULL,
  `telephone` varchar(32) DEFAULT NULL,
  `birth` datetime(3) DEFAULT NULL,
  `email` varchar(64) DEFAULT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  PRIMARY KEY (`user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for params
-- ----------------------------
DROP TABLE IF EXISTS `params`;
CREATE TABLE `params` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
  `field` varchar(255) DEFAULT NULL COMMENT 'key',
  `value` varchar(255) DEFAULT NULL COMMENT 'value',
  `remark` varchar(255) DEFAULT '1' COMMENT '备注',
  `create_time` datetime DEFAULT NULL COMMENT '添加时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- ----------------------------
-- Table structure for point_detail
-- ----------------------------
DROP TABLE IF EXISTS `point_detail`;
CREATE TABLE `point_detail` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
  `send_user_id` varchar(255) DEFAULT NULL COMMENT '发送红包用户id',
  `user_id` varchar(255) DEFAULT NULL COMMENT '用户id',
  `title` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '标题',
  `exchange_time` datetime DEFAULT NULL COMMENT '签到/兑换时间',
  `point` int(11) DEFAULT NULL COMMENT '积分',
  `sort` int(11) unsigned DEFAULT '1' COMMENT '排序',
  `red_packet_id` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '管理红包记录id',
  `client_id` varchar(50) DEFAULT NULL COMMENT '客户端ID',
  `create_time` datetime DEFAULT NULL COMMENT '添加时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=389 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for point_exchange_record
-- ----------------------------
DROP TABLE IF EXISTS `point_exchange_record`;
CREATE TABLE `point_exchange_record` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
  `record_id` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '流水号（user_id+yyyymmddhhmmss+两位随机数)',
  `user_id` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '用户id',
  `title` varchar(255) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '标题',
  `product_id` int(11) DEFAULT NULL COMMENT '商品id',
  `exchange_time` datetime DEFAULT NULL COMMENT '签到/兑换时间',
  `exchange_status` int(11) DEFAULT NULL COMMENT '状态（0：兑换中  1：兑换成功  2：已退还）',
  `exchange_num` int(11) DEFAULT '1' COMMENT '兑换数量',
  `customer_service_id` int(11) DEFAULT '0' COMMENT '客服id',
  `point` int(11) DEFAULT NULL COMMENT '积分',
  `remark` varchar(1000) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '备注',
  `sort` int(11) unsigned DEFAULT '1' COMMENT '排序',
  `create_time` datetime DEFAULT NULL COMMENT '添加时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for product
-- ----------------------------
DROP TABLE IF EXISTS `product`;
CREATE TABLE `product` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
  `title` varchar(255) DEFAULT NULL COMMENT '标题',
  `sub_title` varchar(1000) DEFAULT NULL COMMENT '副标题',
  `directions` text COMMENT '说明',
  `rule_des` text COMMENT '规则',
  `logo` varchar(255) DEFAULT NULL COMMENT 'logo地址',
  `point` int(11) DEFAULT NULL COMMENT '兑换所需积分',
  `store_num` int(11) DEFAULT NULL COMMENT '库存数量',
  `val_start_date` datetime DEFAULT NULL COMMENT '商品有效期',
  `val_end_date` datetime DEFAULT NULL COMMENT '商品有效期',
  `customer_service_id` varchar(255) DEFAULT '0' COMMENT '客服id',
  `sort` int(11) DEFAULT '1' COMMENT '排序',
  `create_time` datetime DEFAULT NULL COMMENT '添加时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=8 DEFAULT CHARSET=utf8mb4 COMMENT='产品表';

-- ----------------------------
-- Table structure for red_packets
-- ----------------------------
DROP TABLE IF EXISTS `red_packets`;
CREATE TABLE `red_packets` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
  `record_id` varchar(255) DEFAULT NULL COMMENT '记录号（user_id+yyyymmddhhmmss+两位随机数)',
  `user_id` int(11) DEFAULT NULL COMMENT '用户id',
  `total_point` int(11) DEFAULT NULL COMMENT '总球币',
  `point` int(11) DEFAULT NULL COMMENT '单个红包球币',
  `count` int(11) DEFAULT NULL COMMENT '实时剩余数量',
  `real_count` int(11) DEFAULT NULL COMMENT '红包个数',
  `val_time` datetime DEFAULT NULL COMMENT '过期时间',
  `remark` varchar(255) DEFAULT NULL COMMENT '文案',
  `create_time` datetime DEFAULT NULL COMMENT '添加时间',
  `update_time` datetime DEFAULT NULL COMMENT '更新时间',
  `is_return` int(11) DEFAULT '0' COMMENT '是否退还（1已退还  0 未退还）',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- ----------------------------
-- Table structure for register_add_friend
-- ----------------------------
DROP TABLE IF EXISTS `register_add_friend`;
CREATE TABLE `register_add_friend` (
  `user_id` varchar(64) NOT NULL,
  PRIMARY KEY (`user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for registers
-- ----------------------------
DROP TABLE IF EXISTS `registers`;
CREATE TABLE `registers` (
  `account` char(255) NOT NULL,
  `password` varchar(255) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  `user_id` varchar(255) DEFAULT NULL,
  `area_code` varchar(255) DEFAULT NULL,
  `invitation_code` varchar(255) DEFAULT NULL,
  `register_ip` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`account`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for site_navigation
-- ----------------------------
DROP TABLE IF EXISTS `site_navigation`;
CREATE TABLE `site_navigation` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
  `title` varchar(100) DEFAULT NULL COMMENT '标题',
  `type_id` int(11) NOT NULL DEFAULT '1' COMMENT '球类ID',
  `logo` varchar(255) DEFAULT NULL COMMENT 'logo',
  `url` text COMMENT '广告链接',
  `content` text COMMENT '描述',
  `sort` int(11) unsigned DEFAULT '1' COMMENT '排序',
  `size` varchar(10) DEFAULT 'min' COMMENT '大小',
  `create_time` int(11) unsigned DEFAULT '0' COMMENT '添加时间',
  `update_time` int(11) unsigned DEFAULT '0' COMMENT '更新时间',
  `mark` tinyint(1) unsigned NOT NULL DEFAULT '1' COMMENT '有效标识(1正常 0删除)',
  `create_user` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '添加人',
  `update_user` int(11) unsigned DEFAULT '0' COMMENT '更新人',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=21 DEFAULT CHARSET=utf8mb4 COMMENT='直播导航表';

-- ----------------------------
-- Table structure for site_navigation_type
-- ----------------------------
DROP TABLE IF EXISTS `site_navigation_type`;
CREATE TABLE `site_navigation_type` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '主键',
  `name` varchar(255) DEFAULT NULL,
  `sort` int(11) unsigned DEFAULT '1' COMMENT '排序',
  `create_time` int(11) unsigned DEFAULT '0' COMMENT '添加时间',
  `update_time` int(11) unsigned DEFAULT '0' COMMENT '更新时间',
  `mark` tinyint(1) unsigned NOT NULL DEFAULT '1' COMMENT '有效标识(1正常 0删除)',
  `create_user` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '添加人',
  `update_user` int(11) unsigned DEFAULT '0' COMMENT '更新人',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8mb4;

-- ----------------------------
-- Table structure for user_ip_limits
-- ----------------------------
DROP TABLE IF EXISTS `user_ip_limits`;
CREATE TABLE `user_ip_limits` (
  `user_id` varchar(64) NOT NULL,
  `ip` varchar(15) NOT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  PRIMARY KEY (`user_id`,`ip`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for user_ip_records
-- ----------------------------
DROP TABLE IF EXISTS `user_ip_records`;
CREATE TABLE `user_ip_records` (
  `user_id` varchar(64) NOT NULL,
  `create_ip` varchar(15) DEFAULT NULL,
  `last_login_time` datetime(3) DEFAULT NULL,
  `last_login_ip` varchar(15) DEFAULT NULL,
  `login_times` int(11) DEFAULT NULL,
  PRIMARY KEY (`user_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for user_ip_white_list
-- ----------------------------
DROP TABLE IF EXISTS `user_ip_white_list`;
CREATE TABLE `user_ip_white_list` (
  `user_id` varchar(64) NOT NULL,
  `ip` varchar(15) NOT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  PRIMARY KEY (`user_id`,`ip`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for users
-- ----------------------------
DROP TABLE IF EXISTS `users`;
CREATE TABLE `users` (
  `user_id` varchar(64) NOT NULL,
  `name` varchar(255) DEFAULT NULL,
  `face_url` varchar(255) DEFAULT NULL,
  `gender` int(11) DEFAULT NULL,
  `phone_number` varchar(32) DEFAULT NULL,
  `birth` datetime(3) DEFAULT NULL,
  `email` varchar(64) DEFAULT NULL,
  `ex` varchar(1024) DEFAULT NULL,
  `status` int(11) DEFAULT NULL,
  `create_time` datetime(3) DEFAULT NULL,
  `app_manger_level` int(11) DEFAULT NULL,
  `global_recv_msg_opt` int(11) DEFAULT NULL,
  `check_in_point` int(11) NOT NULL,
  `check_in_time` bigint(20) DEFAULT NULL,
  `user_type` int(11) DEFAULT NULL,
  `ci_point` bigint(20) DEFAULT NULL,
  `rp_point` bigint(20) DEFAULT NULL,
  `rp_max_user_id` varchar(255) DEFAULT NULL,
  `rp_max_point` bigint(20) DEFAULT NULL,
  PRIMARY KEY (`user_id`,`check_in_point`) USING BTREE,
  UNIQUE KEY `phone_number` (`phone_number`) USING BTREE,
  KEY `create_time` (`create_time`) USING BTREE,
  KEY `check_in_time` (`check_in_time`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

SET FOREIGN_KEY_CHECKS = 1;


```