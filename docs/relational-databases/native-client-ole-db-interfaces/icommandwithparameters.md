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
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 14eebf814d3dbcde2863e117814d3c8a07162945
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  로 시작 하는 데이터베이스 엔진의에서 향상 된 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] icommandwithparameters:: Getparameterinfo 예상된 결과 대 한 보다 정확한 설명의 얻을를 허용 합니다. 이전 버전의 CommandWithParameters::GetParameterInfo 반환 하는 값에서 다를 수 있습니다 이러한 보다 정확한 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 참조 [메타 데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)합니다.  
  
 또한 부터는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]전달 되는 값 icommandwithparameters:: Setparameterinfo를 호출할 때는 *pwszName* 매개 변수는 유효한 식별자 여야 합니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [인터페이스 &#40; OLE db&#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
