---
title: ICommandWithParameters | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea85e526d99e586c2534eee8ab83c6ddc66939db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62643260"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
  로 시작 하는 데이터베이스 엔진의 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 향상 된 기능을 사용 하 여 ICommandWithParameters:: GetParameterInfo를 통해 예상 결과에 대 한 보다 정확한 설명을 얻을 수 있습니다. 이러한 보다 정확한 결과는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 CommandWithParameters:: GetParameterInfo가 반환 하는 값과 다를 수 있습니다. 자세한 내용은 [메타데이터 검색](../native-client/features/metadata-discovery.md)을 참조하세요.  
  
 또한 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 ICommandWithParameters::SetParameterInfo를 호출할 때 *pwszName* 매개 변수에 전달된 값이 유효한 식별자여야 합니다. 자세한 내용은 [Database Identifiers](../databases/database-identifiers.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
