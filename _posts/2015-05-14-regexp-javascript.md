---
layout: post
category: "javascript"
title: "javascript�е�������ʽ"
tags: ["javascript"]
---
������ʽ�������������Ƶã�����������һ��

#### ��js�������Ӧ��
1.�����滻
2.����֤
3.����ƥ��

#### �½�������ʽ

```javascript
	//��һ�ַ�ʽ
	var pattern = new RegExp("box","igm");	//��һ��������ƥ�����ݣ��ڶ��������ǿ�ѡ������i���Դ�Сд,g��ȫ��ƥ��,m�Ǻ��Ի���
	var pattern = /box/igm;
```

#### ����

```javascript
	pattern.test(str);	//���str�ַ����Ƿ�ƥ��pattern,���ز���ֵ
	pattern.exec(str);	//ͨ�����str�ַ��������Ƿ�ƥ��pattern,����һ������,û��ƥ���򷵻�null
```

#### ��ʹ������ƥ����ַ�������

```javascript
	str.match(pattern);	//��������,����ͨ��pattern.length��ȡ����
	str.search(pattern);	//����λ��,type number,�Ҳ�������-1
	str.replace(pattern,'ostr');	//ƥ����滻�ɵڶ�������,����ȫ�ֿ����滻���е�,����ֻ�滻��һ��
	str.split(pattern);	//���ձ��ʽ���ַ����ָ������
```