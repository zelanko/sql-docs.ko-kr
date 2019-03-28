---
title: sp_dsninfo (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e6eacb453fc2f66f4b87790770fa50916916a27c
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527434"
---
# <a name="spdsninfo-transact-sql"></a>sp_dsninfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 서버와 연관된 배포자에서 ODBC 또는 OLE DB 데이터 원본 정보를 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>인수  
`[ @dsn = ] 'dsn'` ODBC DSN 또는 OLE DB 연결 된 서버의 이름이입니다. *dsn* 됩니다 **varchar(128)**, 기본값은 없습니다.  
  
`[ @infotype = ] 'info_type'` 반환할 정보의 유형이입니다. 하는 경우 *info_type* 지정 되지 않았거나 NULL을 지정한 경우 모든 정보 유형이 반환 됩니다. *info_type* 됩니다 **varchar(128)**, 기본값은 NULL 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**DBMS_NAME**|데이터 원본의 공급업체 이름을 나타냅니다.|  
|**DBMS_VERSION**|데이터 원본의 버전을 나타냅니다.|  
|**DATABASE_NAME**|데이터베이스 이름을 나타냅니다.|  
|**SQL_SUBSCRIBER**|데이터 원본이 구독자가 될 수 있는지를 나타냅니다.|  
  
`[ @login = ] 'login'` 데이터 원본에 대 한 로그인이입니다. 데이터 원본에 로그인이 포함되어 있는 경우에는 NULL을 지정하거나 매개 변수를 생략하십시오. *로그인*됩니다 **varchar(128)**, 기본값은 NULL입니다.  
  
`[ @password = ] 'password'` 로그인에 대 한 암호가입니다. 데이터 원본에 로그인이 포함되어 있는 경우에는 NULL을 지정하거나 매개 변수를 생략하십시오. *암호*됩니다 **varchar(128)**, 기본값은 NULL입니다.  
  
`[ @dso_type = ] dso_type` 데이터 원본 유형이입니다. *dso_type* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1** (기본값)|ODBC 데이터 원본|  
|**3**|OLE DB 데이터 원본|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**정보 유형**|**nvarchar(64)**|DBMS_NAME, DBMS_VERSION, DATABASE_NAME, SQL_SUBSCRIBER 등의 정보 유형입니다.|  
|**Value**|**nvarchar(512)**|관련 정보 유형의 값입니다.|  
  
## <a name="remarks"></a>Remarks  
 **sp_dsninfo** 모든 유형의 복제에 사용 됩니다.  
  
 **sp_dsninfo** 복제 또는 쿼리에 대해 데이터베이스를 사용할 수 있는지 여부를 보여 주는 ODBC 또는 OLE DB 데이터 원본 정보를 검색 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_dsninfo**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_enumdsn &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
