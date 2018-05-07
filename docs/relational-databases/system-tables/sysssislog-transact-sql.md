---
title: sysssislog (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
caps.latest.revision: 40
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0f60ec3735bc89c7e729ac6ec01e6f62f126c51f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysssislog-transact-sql"></a>sysssislog(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  런타임에 패키지나 패키지의 태스크 및 컨테이너에 의해 생성되는 각 로깅 항목에 대해 한 행을 포함합니다. 이 테이블은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치할 때 msdb 데이터베이스에 만들어집니다. 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 기록하도록 로깅을 구성하면 이러한 형식의 sysssislog 테이블이 지정한 데이터베이스에 만들어집니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 이 테이블에 로깅 항목을 기록 **만** 패키지 사용 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 공급자입니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|로깅 항목의 고유 식별자입니다.|  
|이벤트|**sysname**|로깅 항목을 생성한 이벤트의 이름입니다.|  
|computer|**nvarchar**|로깅 항목이 생성될 때 패키지가 실행된 컴퓨터입니다.|  
|적용한 후|**nvarchar**|로깅 항목을 생성한 패키지를 실행한 사용자의 이름입니다.|  
|원본(source)|**nvarchar**|로깅 항목을 생성한 패키지에 있는 실행 파일의 이름입니다.|  
|sourceid|**uniqueidentifier**|로깅 항목을 생성한 패키지에 있는 실행 파일의 GUID입니다.|  
|executionid|**uniqueidentifier**|로깅 항목을 생성한 실행 파일의 실행 인스턴스 GUID입니다.|  
|starttime|**datetime**|패키지 실행이 시작된 시간입니다.|  
|endtime|**datetime**|패키지가 완료된 시간입니다.<br /><br /> 이 기능은 구현되지 않았습니다. endtime 열의 값은 항상 starttime 열의 값과 같습니다.|  
|datacode|**int**|일반적으로 컨테이너 또는 태스크를 실행한 결과를 나타내는 선택적 정수 값입니다.|  
|databytes|**image**|추가 정보가 포함된 선택적 바이트 배열입니다.|  
|message|**nvarchar**|이벤트에 대한 설명 및 이벤트 관련 정보입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services & #40; Ssis& #41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
