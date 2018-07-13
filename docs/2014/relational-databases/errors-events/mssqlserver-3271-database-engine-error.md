---
title: MSSQLSERVER_3271 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3271 (Database Engine error)
ms.assetid: 21b8de4b-6624-4163-9561-1a6cc8fe3d51
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a0f6a1583d4437a351b68739ce85bbb5f2154f2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427942"
---
# <a name="mssqlserver3271"></a>MSSQLSERVER_3271
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3271|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DMPIO_IO_ERROR|  
|메시지 텍스트|파일 "%ls"에서 복구할 수 없는 I/O 오류가 발생했습니다: %ls.|  
  
## <a name="explanation"></a>설명  
 이 오류는 백업 또는 복원 작업을 위한 I/O를 수행하는 동안 운영 체제에서 오류가 발생할 때 일어나는 일반적인 오류입니다. 대부분의 경우 원인은 백업 미디어가 꽉 찼기 때문입니다.  
  
 이 오류에는 디스크가 꽉 찼음을 나타내는 운영 체제 텍스트가 추가로 포함될 수 있습니다. 타사의 백업 소프트웨어를 사용하여 백업 또는 복원 작업을 수행하는 경우 백업에 실패했음을 나타내는 메시지가 추가로 발생할 수 있습니다. 이 메시지는 다음 텍스트와 유사합니다.  
  
```  
"2005-08-02 16:05:16.04 spid55 Error: 18210, Severity: 16, State: 1.  
 2005-08-02 16:05:16.04 spid55 BackupVirtualDeviceFile  
::RequestDurableMedia: Flush failure on backup device 'VDINULL'.   
Operating system error 995(The I/O operation has been aborted because   
of either a thread exit or an application request.)."  
```  
  
 이 텍스트는 백업 소프트웨어가 백업 또는 복원 작업의 종료를 요청했음을 나타냅니다.  
  
## <a name="user-action"></a>사용자 동작  
 다음 태스크를 적절하게 수행합니다.  
  
-   오류의 원인을 파악하려면 이 오류 이전에 나오는 기본 시스템 오류 메시지 및 SQL Server 오류 메시지를 검토하십시오.  
  
-   백업 및 복원 미디어에 충분한 공간이 있는지 확인하십시오.  
  
-   타사 백업 및 복원 소프트웨어에서 발생한 오류를 수정하십시오.  
  
  
