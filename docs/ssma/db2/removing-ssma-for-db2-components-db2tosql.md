---
title: DB2 용 SSMA 구성 요소 제거 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6e5d1cd88027dfa3fb4216c93ab4e660ddcc0dc9
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936739"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>DB2 용 SSMA 구성 요소 제거 (DB2ToSQL)
DB2에서로 데이터베이스를 마이그레이션한 후에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 SSMA 구성 요소를 제거 하는 것이 좋습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션된 데이터베이스가 **sysdb** 데이터베이스의 **ssma_DB2** 스키마에서 함수를 더 이상 사용 하지 않는 경우에는에서 확장 팩을 제거 하면 안 됩니다.  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>DB2 용 SSMA 클라이언트 제거  
**프로그램 추가/제거**를 사용 하 여 ssma를 제거할 수 있습니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판에서 **프로그램 추가 또는 제거**를 엽니다.  
  
2.  D b 2 ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 Migration Assistant**을 선택 하 고 **제거**를 클릭 합니다.  
  
3.  SSMA를 제거할 것인지 확인 하려면 **예**를 클릭 합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩 제거  
마이그레이션된 데이터베이스가 **sysdb. ssma_DB2** 스키마의 개체를 사용 하지 않는 것이 확실 한 경우 스키마에서 확장 팩을 삭제 하 여 제거할 수 있습니다. Windows 제거는 없습니다.  
  
## <a name="see-also"></a>참고 항목  
[DB2ToSQL&#41;&#40;DB2 용 SSMA 클라이언트 설치](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[SQL Server &#40;DB2ToSQL&#41;에 SSMA 구성 요소 설치](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
