---
title: sp_db_selective_xml_index (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_selective_xml_index_TSQL
- sp_db_selective_xml_index
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_selective_xml_index procedure
ms.assetid: 017301a2-4a23-4e68-82af-134f3d4892b3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1648cca415f37f9c54f13857d25af90a65372c04
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68108228"
---
# <a name="sp_db_selective_xml_index-transact-sql"></a>sp_db_selective_xml_index(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 선택적 XML 인덱스 기능을 설정 및 해제합니다. 매개 변수 없이 호출할 경우, 특정 데이터베이스에서 선택적 XML 인덱스가 설정되어 있으면 저장 프로시저에서 1을 반환합니다.  
  
> [!NOTE]  
>  이 저장 프로시저를 사용 하 여 선택적 XML 인덱스를 사용 하지 않도록 설정 하려면 [transact-sql&#41;명령 &#40;ALTER DATABASE SET 옵션](../../t-sql/statements/alter-database-transact-sql-set-options.md) 을 사용 하 여 데이터베이스를 단순 복구 모드로 설정 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
  
      sys.sp_db_selective_xml_index[[ @db_name = ] 'db_name'],   
[[ @action = ] 'action']  
```  
  
## <a name="arguments"></a>인수  
`[ @ db_name = ] 'db_name'`선택적 XML 인덱스를 사용 하거나 사용 하지 않도록 설정할 데이터베이스의 이름입니다. *DB_NAME* NULL 인 경우 현재 데이터베이스를 가정 합니다.  
  
`[ @action = ] 'action'`인덱스를 사용 하거나 사용 하지 않을 지 여부를 결정 합니다. ' On ', ' true ', ' off ' 또는 ' f a l s e '를 제외한 다른 값이 전달 되 면 오류가 발생 합니다.  
  
```  
  
Allowed values: 'on', 'off', 'true', 'false'  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 특정 데이터베이스에서 선택적 XML 인덱스를 사용 하는 경우 **1** 입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-enable-selective-xml-index-functionality"></a>A. 선택적 XML 인덱스 기능 설정  
 다음 예에서는 현재 데이터베이스에서 선택적 XML 인덱스를 설정합니다.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'on';  
GO  
```  
  
 다음 예에서는 AdventureWorks2012 데이터베이스에서 선택적 XML 인덱스를 설정합니다.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'true';  
GO  
```  
  
### <a name="b-disable-selective-xml-index-functionality"></a>B. 선택적 XML 인덱스 기능 해제  
 다음 예에서는 현재 데이터베이스에서 선택적 XML 인덱스를 해제합니다.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = NULL  
  , @action = N'off';  
GO  
```  
  
 다음 예에서는 AdventureWorks2012 데이터베이스에서 선택적 XML 인덱스를 해제합니다.  
  
```  
EXECUTE sys.sp_db_selective_xml_index  
    @db_name = N'AdventureWorks2012'  
  , @action = N'false';  
GO  
```  
  
### <a name="c-detect-if-selective-xml-index-is-enabled"></a>C. 선택적 XML 인덱스가 설정되어 있는지 확인  
 다음 예에서는 선택적 XML 인덱스가 설정되어 있는지 확인합니다. 선택적 XML 인덱스가 설정되어 있으면 1이 반환됩니다.  
  
```  
EXECUTE sys.sp_db_selective_xml_index;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SXI&#40;선택적 XML 인덱스&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
