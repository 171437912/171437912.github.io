---
layout:     post
title:      MyBatis��Mapper�ӿ��Լ�Example��ʵ�����������
subtitle:   MyBatis��Mapper�ӿ��Լ�Example��ʵ�����������
date:       2018-04-17
author:     BY
header-img: img/post-bg-BJJ.jpg
catalog: true
tags:
    - BJJ
---


MyBatis��Mapper�ӿ��Լ�Example��ʵ�����������

###  Ŀ¼
-  mapper�ӿ��еķ�������
-  ����	����˵��
-  exampleʵ������
-  ����	˵��
-  Ӧ�þ���
-  ��ѯ
-  ��������
-  ��������
-  ɾ������
- ��ѯ��������

##   mapper�ӿ��еķ�������
mapper�ӿ��еĺ���������

###  ����	����˵��
int countByExample(UserExample example) thorws SQLException	����������
int deleteByPrimaryKey(Integer id) thorws SQLException	������ɾ��
int deleteByExample(UserExample example) thorws SQLException	��������ѯ
String/Integer insert(User record) thorws SQLException	�������ݣ�����ֵΪID��
User selectByPrimaryKey(Integer id) thorws SQLException	��������ѯ
ListselectByExample(UserExample example) thorws SQLException	��������ѯ
ListselectByExampleWithBLOGs(UserExample example) thorws SQLException	��������ѯ������BLOB�ֶΣ���ֻ�е����ݱ��е��ֶ�������Ϊ�����ƵĲŻ������
int updateByPrimaryKey(User record) thorws SQLException	����������
int updateByPrimaryKeySelective(User record) thorws SQLException	����������ֵ��Ϊnull���ֶ�
int updateByExample(User record, UserExample example) thorws SQLException	����������
int updateByExampleSelective(User record, UserExample example) thorws SQLException	����������ֵ��Ϊnull���ֶ�
##  exampleʵ������
mybatis�����򹤳��л�����ʵ����ʵ����Ӧ��example��example��������������൱where����Ĳ��� 
xxxExample example = new xxxExample(); 
Criteria criteria = new Example().createCriteria();

### ����	˵��
example.setOrderByClause(���ֶ��� ASC��);	�����������������DESCΪ����
example.setDistinct(false)	ȥ���ظ���boolean�ͣ�trueΪѡ���ظ��ļ�¼��
criteria.andXxxIsNull	����ֶ�xxxΪnull������
criteria.andXxxIsNotNull	����ֶ�xxx��Ϊnull������
criteria.andXxxEqualTo(value)	���xxx�ֶε���value����
criteria.andXxxNotEqualTo(value)	���xxx�ֶβ�����value����
criteria.andXxxGreaterThan(value)	���xxx�ֶδ���value����
criteria.andXxxGreaterThanOrEqualTo(value)	���xxx�ֶδ��ڵ���value����
criteria.andXxxLessThan(value)	���xxx�ֶ�С��value����
criteria.andXxxLessThanOrEqualTo(value)	���xxx�ֶ�С�ڵ���value����
criteria.andXxxIn(List<��>)	���xxx�ֶ�ֵ��List<��>����
criteria.andXxxNotIn(List<��>)	���xxx�ֶ�ֵ����List<��>����
criteria.andXxxLike(��%��+value+��%��)	���xxx�ֶ�ֵΪvalue��ģ����ѯ����
criteria.andXxxNotLike(��%��+value+��%��)	���xxx�ֶ�ֵ��Ϊvalue��ģ����ѯ����
criteria.andXxxBetween(value1,value2)	���xxx�ֶ�ֵ��value1��value2֮������
criteria.andXxxNotBetween(value1,value2)	���xxx�ֶ�ֵ����value1��value2֮������
###  Ӧ�þ���
####  ��ѯ
�� selectByPrimaryKey()

User user = XxxMapper.selectByPrimaryKey(100); //�൱��select * from user where id = 100
1
�� selectByExample() �� selectByExampleWithBLOGs()

UserExample example = new UserExample();
Criteria criteria = example.createCriteria();
criteria.andUsernameEqualTo("wyw");
criteria.andUsernameIsNull();
example.setOrderByClause("username asc,email desc");
List<?>list = XxxMapper.selectByExample(example);
//�൱�ڣ�select * from user where username = 'wyw' and  username is null order by username asc,email desc
1
2
3
4
5
6
7
ע����iBator���򹤳����ɵ��ļ�XxxExample.java�а���һ��static���ڲ���Criteria��Criteria�еķ����Ƕ���SQL ���where��Ĳ�ѯ������

####  ��������
��insert()

User user = new User();
user.setId("dsfgsdfgdsfgds");
user.setUsername("admin");
user.setPassword("admin")
user.setEmail("wyw@163.com");
XxxMapper.insert(user);
//�൱�ڣ�insert into user(ID,username,password,email) values ('dsfgsdfgdsfgds','admin','admin','wyw@126.com');
1
2
3
4
5
6
7
####  ��������
��updateByPrimaryKey()

User user =new User();
user.setId("dsfgsdfgdsfgds");
user.setUsername("wyw");
user.setPassword("wyw");
user.setEmail("wyw@163.com");
XxxMapper.updateByPrimaryKey(user);
//�൱�ڣ�update user set username='wyw', password='wyw', email='wyw@163.com' where id='dsfgsdfgdsfgds'
1
2
3
4
5
6
7
��updateByPrimaryKeySelective()

User user = new User();
user.setId("dsfgsdfgdsfgds");
user.setPassword("wyw");
XxxMapper.updateByPrimaryKey(user);
//�൱�ڣ�update user set password='wyw' where id='dsfgsdfgdsfgds'
1
2
3
4
5
�� updateByExample() �� updateByExampleSelective()

UserExample example = new UserExample();
Criteria criteria = example.createCriteria();
criteria.andUsernameEqualTo("admin");
User user = new User();
user.setPassword("wyw");
XxxMapper.updateByPrimaryKeySelective(user,example);
//�൱�ڣ�update user set password='wyw' where username='admin'
1
2
3
4
5
6
7
updateByExample()�������е��ֶΣ������ֶ�Ϊnull��Ҳ���£�����ʹ�� updateByExampleSelective()��������µ��ֶ�

####  ɾ������
��deleteByPrimaryKey()

XxxMapper.deleteByPrimaryKey(1);  //�൱�ڣ�delete from user where id=1
1
��deleteByExample()

UserExample example = new UserExample();
Criteria criteria = example.createCriteria();
criteria.andUsernameEqualTo("admin");
XxxMapper.deleteByExample(example);
//�൱�ڣ�delete from user where username='admin'
1
2
3
4
5
####  ��ѯ��������
��countByExample()

UserExample example = new UserExample();
Criteria criteria = example.createCriteria();
criteria.andUsernameEqualTo("wyw");
int count = XxxMapper.countByExample(example);
//�൱�ڣ�select count(*) from user where username='wyw'