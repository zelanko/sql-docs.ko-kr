---
description: sysssislog(Transact-SQL)
title: sysssislog (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9aef51cb3297cd83b68fa42c71dcd993fb418830
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473110"
---
# <a name="sysssislog-transact-sql"></a>sysssislog(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  런타임에 패키지나 패키지의 태스크 및 컨테이너에 의해 생성되는 각 로깅 항목에 대해 한 행을 포함합니다. 이 테이블은를 설치할 때 msdb 데이터베이스에 만들어집니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 기록하도록 로깅을 구성하면 이러한 형식의 sysssislog 테이블이 지정한 데이터베이스에 만들어집니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 패키지에서 로그 공급자를 사용 하는 경우에 **만** 이 테이블의 로깅 항목을 작성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|로깅 항목의 고유 식별자입니다.|  
|event|**sysname**|로깅 항목을 생성한 이벤트의 이름입니다.|  
|computer|**nvarchar**|로깅 항목이 생성될 때 패키지가 실행된 컴퓨터입니다.|  
|operator|**nvarchar**|로깅 항목을 생성한 패키지를 실행한 사용자의 이름입니다.|  
|source|**nvarchar**|로깅 항목을 생성한 패키지에 있는 실행 파일의 이름입니다.|  
|sourceid|**uniqueidentifier**|로깅 항목을 생성한 패키지에 있는 실행 파일의 GUID입니다.|  
|executionid|**uniqueidentifier**|로깅 항목을 생성한 실행 파일의 실행 인스턴스 GUID입니다.|  
|starttime|**datetime**|패키지 실행이 시작된 시간입니다.|  
|endtime|**datetime**|패키지가 완료된 시간입니다.<br /><br /> 이 기능은 구현되지 않았습니다. endtime 열의 값은 항상 starttime 열의 값과 같습니다.|  
|datacode|**int**|일반적으로 컨테이너 또는 태스크를 실행한 결과를 나타내는 선택적 정수 값입니다.|  
|databytes|**image**|추가 정보가 포함된 선택적 바이트 배열입니다.|  
|message|**nvarchar**|이벤트에 대한 설명 및 이벤트 관련 정보입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
