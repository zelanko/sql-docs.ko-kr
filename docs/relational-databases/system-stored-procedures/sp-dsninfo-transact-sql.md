---
title: sp_dsninfo (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dsninfo
- sp_dsninfo_TSQL
helpviewer_keywords:
- sp_dsninfo
ms.assetid: 34648615-814b-42bc-95a3-50e86b42ec4d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 59d0b995103ab01d3bf3b7ec5336ad16b97b1e6f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881747"
---
# <a name="sp_dsninfo-transact-sql"></a>sp_dsninfo(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 서버와 연관된 배포자에서 ODBC 또는 OLE DB 데이터 원본 정보를 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>인수  
`[ @dsn = ] 'dsn'`ODBC DSN 또는 OLE DB 연결 된 서버의 이름입니다. *dsn* 은 **varchar (128)** 이며 기본값은 없습니다.  
  
`[ @infotype = ] 'info_type'`반환할 정보의 형식입니다. *Info_type* 지정 하지 않거나 NULL을 지정 하면 모든 정보 유형이 반환 됩니다. *info_type* 는 **varchar (128)** 이며 기본값은 NULL이 고 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**DBMS_NAME**|데이터 원본의 공급업체 이름을 나타냅니다.|  
|**DBMS_VERSION**|데이터 원본의 버전을 나타냅니다.|  
|**DATABASE_NAME**|데이터베이스 이름을 나타냅니다.|  
|**SQL_SUBSCRIBER**|데이터 원본이 구독자가 될 수 있는지를 나타냅니다.|  
  
`[ @login = ] 'login'`데이터 원본에 대 한 로그인입니다. 데이터 원본에 로그인이 포함되어 있는 경우에는 NULL을 지정하거나 매개 변수를 생략하십시오. *login*은 **varchar (128)** 이며 기본값은 NULL입니다.  
  
`[ @password = ] 'password'`로그인에 대 한 암호입니다. 데이터 원본에 로그인이 포함되어 있는 경우에는 NULL을 지정하거나 매개 변수를 생략하십시오. *암호*는 **varchar (128)** 이며 기본값은 NULL입니다.  
  
`[ @dso_type = ] dso_type`데이터 원본 유형입니다. *dso_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1** (기본값)|ODBC 데이터 원본|  
|**3**|OLE DB 데이터 원본|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**정보 유형**|**nvarchar (64)**|DBMS_NAME, DBMS_VERSION, DATABASE_NAME, SQL_SUBSCRIBER 등의 정보 유형입니다.|  
|**값**|**nvarchar(512)**|관련 정보 유형의 값입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_dsninfo** 은 모든 유형의 복제에 사용 됩니다.  
  
 **sp_dsninfo** 은 데이터베이스를 복제 또는 쿼리에 사용할 수 있는지 여부를 표시 하는 ODBC 또는 OLE DB 데이터 원본 정보를 검색 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_dsninfo**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_enumdsn &#40;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
