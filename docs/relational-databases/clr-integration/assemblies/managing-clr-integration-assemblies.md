---
title: CLR 통합 어셈블리 관리 | Microsoft Docs
description: SQL Server에서 관리 되는 DLL 어셈블리를 호스트할 수 있습니다.  어셈블리를 등록, 변경 및 삭제할 수 있으며 관련 파일 및 사용 권한도 관리할 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
author: rothja
ms.author: jroth
ms.openlocfilehash: f26a05c999a683bacbda6ffc0cb9da23b20595bb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717918"
---
# <a name="managing-clr-integration-assemblies"></a>CLR 통합 어셈블리 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  관리 코드는 컴파일한 다음 어셈블리라는 단위로 배포합니다. 어셈블리는 DLL이나 실행 파일(.exe)로 패키지됩니다. 실행 파일은 독립적으로 실행할 수 있는 반면 DLL은 기존 애플리케이션 내에서 호스팅해야 합니다. 관리 되는 DLL 어셈블리를에 로드 하 여 호스팅할 수 있습니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 어셈블리를 프로세스에 로드하여 사용하려면 먼저 CREATE ASSEMBLY 문을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 어셈블리를 등록해야 합니다. ALTER ASSEMBLY 문을 사용하여 어셈블리를 최신 버전에서 업데이트하거나 DROP ASSEMBLY 문을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 제거할 수도 있습니다.  
  
 어셈블리 정보는 어셈블리가 설치 된 데이터베이스의 **sys. assembly_files** 테이블에 저장 됩니다. **Assembly_files** 테이블에는 다음 열이 포함 되어 있습니다.  
  
|Column|설명|  
|------------|-----------------|  
|assembly_id|어셈블리에 대해 정의되는 식별자입니다. 해당 어셈블리와 관련한 모든 개체에 이 번호가 할당됩니다.|  
|name|개체 이름입니다.|  
|file_id|지정 된 **assembly_id** 와 연결 된 첫 번째 개체의 값이 1 인 각 개체를 식별 하는 숫자입니다. 여러 개체가 동일한 **assembly_id**와 연결 된 경우 각 후속 **file_id** 값은 1 씩 증가 합니다.|  
|콘텐츠|어셈블리 또는 파일의 16진수 표현입니다.|  
  
## <a name="in-this-section"></a>섹션 내용  
 [어셈블리 만들기](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 SAFE, EXTERNAL_ACCESS 및 UNSAFE CLR 어셈블리를 만드는 방법에 대해 설명합니다.  
  
 [어셈블리 변경](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 CLR 어셈블리를 업데이트하는 방법에 대해 설명합니다.  
  
 [어셈블리 삭제](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 CLR 어셈블리를 삭제하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CLR 통합 보안](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [CLR 통합 코드 액세스 보안](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
  
