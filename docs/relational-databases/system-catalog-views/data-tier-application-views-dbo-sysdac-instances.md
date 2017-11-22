---
title: dbo.sysdac_instances (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysdac_instances_TSQL
- sysdac_instances
- sysdac_instances_TSQL
- dbo.sysdac_instances
dev_langs: TSQL
helpviewer_keywords:
- dbo.sysdac_instances
- sysdac_instances
ms.assetid: 28285f3d-3889-439f-8b24-3bdef08e46b4
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 197eb0d8887f56d77c5851403f2914712a757bbd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="data-tier-application-views---dbosysdacinstances"></a>데이터 계층 응용 프로그램 보기-dbo.sysdac_instances
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 배포된 DAC(데이터 계층 응용 프로그램) 인스턴스마다 하나의 행을 표시합니다. sysdac_instances는 msdb 데이터베이스의 dbo 스키마에 속합니다. 다음 표에서 sysdac_instances 보기의 열에 설명 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|DAC 인스턴스의 식별자입니다.|  
|instance_name|**sysname**|DAC를 배포할 때 지정된 DAC 인스턴스의 이름입니다.|  
|type_name|**sysname**|DAC 패키지를 만들 때 지정된 DAC의 이름입니다.|  
|type_version|**nvarchar(64)**|DAC 패키지를 만들 때 지정된 DAC의 버전입니다.|  
|description|**nvarchar(4000)**|DAC 패키지를 만들 때 작성된 DAC에 대한 설명입니다.|  
|type_stream|**varbinary(max)**|DAC에 포함된 테이블 및 뷰와 같은 논리 개체의 인코딩된 표현을 포함하는 비트 스트림입니다.|  
|date_created|**datetime**|DAC 인스턴스를 만든 날짜와 시간입니다.|  
|created_by|**sysname**|DAC 인스턴스를 만든 사람의 로그인 정보입니다.|  
|database_name|**sysname**|DAC 인스턴스에 대해 만든 데이터베이스의 이름입니다.|  
  
## <a name="remarks"></a>주의  
 DAC는 응용 프로그램에 사용되는 테이블 및 뷰 같은 논리 데이터 계층 개체의 정의인 DAC 유형을 포함합니다. DAC 패키지는 DAC를 배포하는 데 사용되는 파일입니다. DAC 패키지는 DAC 유형에 포함된 모든 논리 개체의 표현을 포함합니다. DAC 패키지를 사용하여 하나 이상의 DAC 복사본 또는 인스턴스를 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 배포할 수 있습니다. 동일한 DAC 패키지에서 배포된 각 DAC 인스턴스는 동일한 유형을 공유하지만 고유한 인스턴스 이름 및 식별자가 할당됩니다.  
  
## <a name="permissions"></a>Permissions  
 모든 열을 보려면 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다. public 역할의 멤버는 instance_name, description 및 type_version 열을 볼 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 계층 응용 프로그램](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [데이터 계층 응용 프로그램 뷰 &#40; Transact SQL &#41;](http://msdn.microsoft.com/library/0de01328-d7a6-4677-b7a0-dcd3098c23d4)  
  
  
