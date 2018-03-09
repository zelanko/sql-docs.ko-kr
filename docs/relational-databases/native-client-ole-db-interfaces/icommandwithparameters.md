---
title: ICommandWithParameters | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04f369ba934f768ddd94754406b4ce0915e3018b
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  로 시작 하는 데이터베이스 엔진의에서 향상 된 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] icommandwithparameters:: Getparameterinfo 예상된 결과 대 한 보다 정확한 설명의 얻을를 허용 합니다. 이전 버전의 CommandWithParameters::GetParameterInfo 반환 하는 값에서 다를 수 있습니다 이러한 보다 정확한 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [Metadata Discovery](../../relational-databases/native-client/features/metadata-discovery.md)를 참조하십시오.  
  
 또한 부터는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]전달 되는 값 icommandwithparameters:: Setparameterinfo를 호출할 때는 *pwszName* 매개 변수는 유효한 식별자 여야 합니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [인터페이스 &#40; OLE db&#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
