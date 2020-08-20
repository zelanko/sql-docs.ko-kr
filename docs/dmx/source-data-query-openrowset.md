---
description: '&lt;원본 데이터 쿼리 &gt; -OPENROWSET'
title: OPENROWSET (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8da3686e7772b7e997690d509c8092917635497a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500791"
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;원본 데이터 쿼리 &gt; -OPENROWSET
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  원본 데이터 쿼리를 외부 공급자에 대한 쿼리로 바꿉니다. INSERT, SELECT FROM 예측 조인 및 SELECT FROM 자연 예측 조인 문에서 **OPENROWSET**을 지원 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>인수  
 *provider_name*  
 OLE DB 공급자 이름입니다.  
  
 *provider_string*  
 지정한 공급자에 대한 OLE DB 연결 문자열입니다.  
  
 *query_syntax*  
 행 집합을 반환하는 쿼리 구문입니다.  
  
## <a name="remarks"></a>설명  
 데이터 마이닝 공급자는 *provider_name* 및 *provider_string를* 사용 하 여 데이터 원본 개체에 대 한 연결을 설정 하 고 *query_syntax* 에 지정 된 쿼리를 실행 하 여 원본 데이터에서 행 집합을 검색 합니다.  
  
## <a name="examples"></a>예제  
 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] SELECT 문을 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 데이터베이스에서 데이터를 검색할 때 PREDICTION JOIN 문 내에서 다음 예를 사용할 수 있습니다.  
  
```  
OPENROWSET  
(  
'SQLOLEDB.1',  
'Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security     Info=False;Initial Catalog=AdventureWorksDW2012;Data Source=localhost',  
'SELECT TOP 1000 * FROM vTargetMail'  
)  
```  
  
## <a name="see-also"></a>참고 항목  
 [&#60;원본 데이터 쿼리&#62;](../dmx/source-data-query.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
