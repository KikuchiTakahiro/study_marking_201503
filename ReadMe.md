#  2015�N3���x�ۑ�

##Lv.1, Lv.2 ����
*��  
�E���[�U�[�e�[�u��(USERS)�͓����(JOINED_DATE)�Ƒމ��(LEFT_DATE)�������Ă���  
�E�މ�Ă��Ȃ����[�U�[�̏ꍇ�A�މ���ɂ�NULL������*

��**���[�U�[���̑������m�F���邽�߂ɁA���t�P�ʂœ�������[�U�[�̐l���Ƒމ�����[�U�[�̐l�����ꗗ���������B  
�ǂ�����Ύ擾�ł��邩�H(1-1)**


**���[�U�[�e�[�u��(USERS)**  
UID(��L�[)	JOINED	_DATE	LEFT_DATE  
1		 2015-03-01	2015-03-10  
2		2015-03-01	2015-03-05  
3		2015-03-03	NULL  
4		2015-03-03	2015-03-10  
5		2015-03-10	NULL
  
**���҂���o�͌���**  
DATE  JOINED_COUNT�@LEFT_COUNT  
2015-03-01�@2	�@�@�@�@�@0  
2015-03-03�@2	�@�@�@�@�@0  
2015-03-05�@0	�@�@�@�@�@1  
2015-03-10�@1	�@�@�@�@�@2  

*�X�L�[�}�쐬�p��SQL*  
>CREATE TABLE USERS (  
>�@  UID�@ INTEGER�@PRIMARY KEY,  
>�@  JOINED�@_DATE�@DATE NOT NULL,  
>�@  LEFT_DATE DATE NULL  
>);  
>  
>INSERT INTO USERS VALUES (1, '2015-03-01', '2015-03-10');    
>INSERT INTO USERS VALUES (2, '2015-03-01', '2015-03-05');  
>INSERT INTO USERS VALUES (3, '2015-03-03', NULL);  
>INSERT INTO USERS VALUES (4, '2015-03-03', '2015-03-10');  
>INSERT INTO USERS VALUES (5, '2015-03-10', NULL);  
  
**�����̓����_�ł̉�������擾���Ă��������B(1-2)** 
    
**���҂���o�͌���**  
DATE�@�@�@�@JOINED_COUNT�@�@�@�@ LEFT_COUNT�@�@�@�@ USER_COUNT  
2015-03-01  2	         0	    2  
2015-03-03  2	         0	    4
2015-03-05  0	         1	    3
2015-03-10  1	         2	    2

##Lv.2�̕��͈ȉ����Ώ�  �@�@  
��  
�E�C�x���g�ƃX�P�W���[���Ƃ�����̃e�[�u��������B  
�E�C�x���g�͕����̃X�P�W���[���������Ƃ��ł���B  
�E�X�P�W���[�����ꌏ�������Ȃ��C�x���g������i�X�P�W���[������̃C�x���g�j�B  
�E�X�P�W���[���ɂ͒��ߐ؂�����ݒ肳��Ă���B  
�E�C�x���g�P�ʂœ������ߐ؂���͕������݂��Ȃ����̂Ƃ���B  
 
**�����̂悤�ȏ����ŃC�x���g�ƃX�P�W���[���̈ꗗ���o�������B(2-1)**  
 �E�V�X�e�����t�ȍ~�ɒ��ߐ؂��������A�܂��̓X�P�W���[������̃C�x���g�݂̂�\������B  
 �E�X�P�W���[������������C�x���g�̓V�X�e�����t�ɍł��߂����ߐ؂���̃X�P�W���[���݂̂�\������B  
 �E���ߐ؂�����ɕ��ёւ���i���ߐ؂�����߂��قǏ�j�B�������X�P�W���[������ł���Έ�ԉ��ɕ\������B  
 �E���ߐ؂���������ł���΃C�x���gID���ɕ��ёւ���iID�����������̂قǏ�j�B  
  
*�C�x���g�e�[�u��*  
UID(��L�[)	EVENT_NAME  
1		Completed event  
2		No schedule event  
3		Continuing event  
4		Future event 1  
5		Future event 2  
  
*�X�P�W���[���e�[�u��*  
UID(��L�[)	EVENT_ID(�O���L�[)�@	DUE_DATE
1		1	�@		2015/04/23  
2		3	�@		2015/04/01  
3		3	�@		2015/05/01  
4		3	�@		2015/06/01  
5		4	�@		2015/04/24  
6		4	�@		2015/04/25  
7		5	�@		2015/04/24  

**���҂���o�͌���(�V�X�e�����t�� 2015/04/24 �̏ꍇ)**  
EVENT_ID�@EVENT_NAME	�@�@�@SCHEDULE_ID�@�@DUE_DATE  
4	�@Future event 1�@�@�@5�@�@�@�@	�@�@ 2015/04/24  
5	�@Future event 2�@�@�@7	�@�@�@�@�@�@ 2015/04/24  
3	�@Continuing event�@�@3	�@�@�@�@�@�@ 2015/05/01  
2	�@No schedule event		

�V�X�e�����t�͕֋X�I�Ɉȉ���SQL�Ŏ擾�ł���l�Ƃ���B  
SELECT MAX(SYSDATE) FROM DUMMY_SYSDATE  
  
*�X�L�[�}�쐬�p��SQL*  

>CREATE TABLE EVENTS (  
>�@�@UID integer PRIMARY KEY  
> �@�@ ,EVENT_NAME varchar(50)  
>);

>INSERT INTO EVENTS VALUES (1,'Completed event');  
>INSERT INTO EVENTS VALUES (2,'No schedule event');  
>INSERT INTO EVENTS VALUES (3,'Continuing event');  
>INSERT INTO EVENTS VALUES (4,'Future event 1');  
>INSERT INTO EVENTS VALUES (5,'Future event 2');  

>CREATE TABLE SCHEDULES (  
>�@UID integer PRIMARY KEY  
>�@,EVENT_ID integer  
>�@ ,DUE_DATE date  
>);

>INSERT INTO SCHEDULES VALUES (1,1,'2015/04/23');  
>INSERT INTO SCHEDULES VALUES (2,3,'2015/04/01');  
>INSERT INTO SCHEDULES VALUES (3,3,'2015/05/01');  
>INSERT INTO SCHEDULES VALUES (4,3,'2015/06/01');  
>INSERT INTO SCHEDULES VALUES (5,4,'2015/04/24');  
>INSERT INTO SCHEDULES VALUES (6,4,'2015/04/25');  
>INSERT INTO SCHEDULES VALUES (7,5,'2015/04/24');  

>CREATE TABLE DUMMY_SYSDATE (  
>�@UID integer PRIMARY KEY  
>�@,SYSDATE date  
>);  

>INSERT INTO DUMMY_SYSDATE VALUES (1,'2015/04/24');  
  
��  
�E�Ј��Ə��������Ƃ�����̃e�[�u��������B  
�E�Ј���1���ȏ�̏��������������B  
�E���������ɂ͂��̎Ј�������܂łɏ������Ă��������̗������ۑ������B  
�E���������ɂ͊J�n�����ݒ肳��Ă���B  
�E������������������ꍇ�A�J�n�����ŐV�̗��������݂̕�����\���B  

**������IT����ɏ������Ă���Ј��̈ꗗ���擾����ɂ͂ǂ�����Ηǂ����B(2-2)**
  
*�Ј��e�[�u��(EMPLOYEES)*  
UID(��L�[)	EMPLOYEE_NAME  
1		John  
2		Mary  
3		Tom  
  
*���������e�[�u��(SECTION_HISTORIES)*  
UID(��L�[)	EMPLOYEE_ID(�O���L�[)	START_DATE	SECTION_NAME  
1		1			2014/01/01	Sales  
2		2			2014/01/01	IT  
3		3			2014/01/01	IT  
4		1			2015/01/01	IT  
5		2			2015/01/01	Sales  
  
*�⑫*  
John(EMPLOYEE_ID: 1)�̌��݂̕�����IT  
Mary(EMPLOYEE_ID: 2)�̌��݂̕�����Sales  
Tom (EMPLOYEE_ID: 3)�̌��݂̕�����IT  
  
**���҂���o�͌���**  
EMPLOYEE_ID	EMPLOYEE_NAME	SECTION_NAME	START_DATE    
1	�@�@�@�@John	        IT		2015/01/01    
3		Tom	        IT		2014/01/01  

_�⑫_  
�\�[�g����EMPLOYEE_ID�Ƃ���

_�X�L�[�}�쐬�p��SQL_�@�@

>CREATE TABLE EMPLOYEES (    
>�@�@UID integer PRIMARY KEY  
>�@�@,EMPLOYEE_NAME varchar(50)  
>);  
  
>INSERT INTO EMPLOYEES VALUES (1,'John');  
>INSERT INTO EMPLOYEES VALUES (2,'Mary');  
>INSERT INTO EMPLOYEES VALUES (3,'Tom');  

>CREATE TABLE SECTION_HISTORIES (  
>  UID integer PRIMARY KEY  
>  ,EMPLOYEE_ID integer  
>  ,START_DATE date  
>  ,SECTION_NAME varchar(50)  
>);  
  
>INSERT INTO SECTION_HISTORIES VALUES (1,1,'2014/01/01', 'Sales');  
>INSERT INTO SECTION_HISTORIES VALUES (2,2,'2014/01/01', 'IT');  
>INSERT INTO SECTION_HISTORIES VALUES (3,3,'2014/01/01', 'IT');  
>INSERT INTO SECTION_HISTORIES VALUES (4,1,'2015/01/01', 'IT');  
>INSERT INTO SECTION_HISTORIES VALUES (5,2,'2015/01/01', 'Sales');  


