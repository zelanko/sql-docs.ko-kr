---
title: OPENQUERY (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a075f314af0eb8ea2eb0bc941ada0bc38e22fec3
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970430"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;원본 데이터 쿼리 &gt; -OPENQUERY
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  원본 데이터 쿼리를 기존 데이터 원본에 대한 쿼리로 바꿉니다. INSERT, SELECT FROM 예측 조인 및 SELECT FROM 자연 예측 조인 문에서 **OPENQUERY**를 지원 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>인수  
 *명명 된 데이터 원본*  
 데이터베이스에 있는 데이터 원본 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 입니다.  
  
 *쿼리 구문*  
 행 집합을 반환하는 쿼리 구문입니다.  
  
## <a name="remarks"></a>설명  
 **OPENQUERY** 는 데이터 원본 사용 권한을 지원 하 여 외부 데이터에 보다 안전 하 게 액세스할 수 있는 방법을 제공 합니다. 연결 문자열은 데이터 원본에 저장되어 있으므로 관리자는 데이터 원본의 속성을 사용하여 데이터에 대한 액세스를 관리할 수 있습니다. 데이터 원본에 대 한 자세한 내용은 [지원 되는 데이터 원본 &#40;SSAS-다차원&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional)를 참조 하세요.  
  
 **MDSCHEMA_INPUT_DATASOURCES** 스키마 행 집합을 쿼리하여 서버에서 사용할 수 있는 데이터 원본 목록을 가져올 수 있습니다. **MDSCHEMA_INPUT_DATASOURCES**사용에 대 한 자세한 내용은 [MDSCHEMA_INPUT_DATASOURCES 행 집합](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126243(v=sql.110))을 참조 하세요.  
  
 다음 DMX 쿼리를 사용하여 현재 Analysis Services 데이터베이스의 데이터 원본 목록을 반환할 수도 있습니다.  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스에 이미 정의 되어 있는 MyDS 데이터 원본을 사용 하 여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 대 한 연결을 만들고 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] **vtargetmail** 뷰를 쿼리 합니다.  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>참고 항목  
 [&#60;원본 데이터 쿼리&#62;](../dmx/source-data-query.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
