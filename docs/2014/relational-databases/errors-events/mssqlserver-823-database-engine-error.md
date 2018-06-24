---
title: MSSQLSERVER_823 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
caps.latest.revision: 24
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a3889444fb2c605bccd36d30dbe324f220bbe942
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081348"
---
# <a name="mssqlserver823"></a>MSSQLSERVER_823
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|823|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|B_HARDERR|  
|메시지 텍스트|파일 '%ls'의 오프셋 %#016I64x에서 %S_MSG 중 운영 체제에서 SQL Server에 대한 오류 %ls을(를) 반환했습니다. SQL Server 오류 로그 및 시스템 이벤트 로그의 추가 메시지에서 더 자세한 정보를 얻을 수 있습니다. 이는 데이터베이스 무결성을 위협하는 심각한 시스템 수준의 오류 상태이며 즉시 수정해야 합니다. 전체 데이터베이스 일관성 확인(DBCC CHECKDB)을 완료하십시오. 이 오류는 여러 요인으로 인해 발생할 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.|  
  
## <a name="explanation"></a>설명  
 Windows 읽기 또는 쓰기 요청이 실패했습니다. Windows에서 반환하는 오류 코드와 해당 텍스트가 메시지에 삽입됩니다. 읽기 작업의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 읽기 요청을 이미 4번 다시 시도했을 수도 있습니다. 이 오류는 하드웨어 오류로 인해 주로 발생하지만 장치 드라이버로 인해 발생할 수도 있습니다. 오류 823에 대한 자세한 내용은 [http://support.microsoft.com/kb/828339](http://support.microsoft.com/kb/828339)를 참조하세요. I/O 오류에 대한 자세한 내용은 [Microsoft SQL Server I/O Basics, Chapter 2](http://go.microsoft.com/fwlink/?LinkId=69370)(Microsoft SQL Server I/O 기본 사항, 2장)를 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
 시스템 이벤트 로그에서 추가 정보를 확인하십시오. 원인 및 수정 동작을 확인하려면 하드웨어 제조업체 또는 Microsoft 고객 서비스 지원 센터에 문의하십시오. 하드웨어 오류를 수정한 후에는 모든 데이터베이스를 복원하고 DBCC CHECKDB를 실행하십시오.  
  
  