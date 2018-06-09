---
title: SSMA DB2 구성 요소 (DB2ToSQL)에 대 한 제거 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 330ce4dee20972148ff74d85e892d879e8b5203a
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34775369"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>SSMA DB2 구성 요소 (DB2ToSQL)에 대 한 제거
완료 했을 때 데이터베이스를 d b 2에서 마이그레이션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA 구성 요소를 제거 해야 할 경우가 있습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있습니다. 그러나 제거해 서는 안에서 확장 팩 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 마이그레이션된 데이터베이스의 함수를 더 이상 사용 하지 않는 한는 **ssma_DB2** 의 스키마는 **sysdb** 데이터베이스입니다.  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>SSMA DB2 클라이언트에 대 한 제거  
SSMA를 사용 하 여 제거할 수 있습니다 **프로그램 추가 / 제거**합니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판을 열고 **프로그램 추가 / 제거**합니다.  
  
2.  선택  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for d b 2**, 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 SSMA를 제거 하려면 클릭 하십시오 **예**합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩을 제거  
마이그레이션된 데이터베이스의 개체를 사용 하지 마십시오 하려는 경우에 **sysdb.ssma_DB2** 스키마를 스키마에서 삭제 하 여 확장 팩을 제거할 수의 배포는 없는 Windows 제거  
  
## <a name="see-also"></a>관련 항목  
[SSMA DB2 클라이언트에 대 한 설치 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[SQL Server에 SSMA 구성 요소 설치 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
