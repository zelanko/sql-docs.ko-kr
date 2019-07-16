---
title: SSMA 용 DB2 구성 요소 제거 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 25c8222009c2ea9358c0bab2ad5ae077588fb3cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060091"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>SSMA 용 DB2 구성 요소 제거 (DB2ToSQL)
완료 했을 때를 DB2에서 데이터베이스를 마이그레이션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 SSMA 구성 요소를 제거 하는 것이 좋습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있습니다. 확장 팩을 제거 하면 안 되는 반면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션된 데이터베이스의 함수를 더 이상 사용 하지 않는 한는 **ssma_DB2** 의 스키마를 **sysdb** 데이터베이스입니다.  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>SSMA DB2 클라이언트에 대 한 제거  
SSMA를 사용 하 여 제거할 수 있습니다 **프로그램 추가 / 제거**합니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판에서 엽니다 **프로그램 추가 / 제거**합니다.  
  
2.  선택  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for DB2**를 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 SSMA를 제거 하려면 클릭 하십시오 **예**합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩을 제거  
마이그레이션된 데이터베이스의 개체를 사용 하지 마십시오 확실 합니다 **sysdb.ssma_DB2** 스키마, 스키마에서 삭제 하 여 확장 팩을 제거할 수 있습니다-이 없는 Windows 제거  
  
## <a name="see-also"></a>관련 항목  
[클라이언트가 DB2 용 SSMA 설치 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[SQL Server에 SSMA 구성 요소를 설치 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
