---
title: CLR 통합 어셈블리 관리 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 1e65bb5c651862a82d78faede158234d20392c1c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62919691"
---
# <a name="managing-clr-integration-assemblies"></a>CLR 통합 어셈블리 관리
  관리 코드는 컴파일한 다음 어셈블리라는 단위로 배포합니다. 어셈블리는 DLL이나 실행 파일(.exe)로 패키지됩니다. 실행 파일은 독립적으로 실행할 수 있는 반면 DLL은 기존 애플리케이션 내에서 호스팅해야 합니다. 관리 되는 DLL 어셈블리를에 로드 하 여 [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]호스팅할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]CREATE ASSEMBLY 문을 사용 하는 데이터베이스는 프로세스에서 로드 하 고 사용할 수 있습니다. ALTER ASSEMBLY 문을 사용하여 어셈블리를 최신 버전에서 업데이트하거나 DROP ASSEMBLY 문을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 제거할 수도 있습니다.  
  
 어셈블리 정보는 어셈블리가 설치된 데이터베이스의 `sys.assembly_files` 테이블에 저장됩니다. `sys.assembly_files` 테이블에는 다음 열이 있습니다.  
  
|열|Description|  
|------------|-----------------|  
|assembly_id|어셈블리에 대해 정의되는 식별자입니다. 해당 어셈블리와 관련한 모든 개체에 이 번호가 할당됩니다.|  
|name|개체 이름입니다.|  
|file_id|각 개체를 식별하는 번호이며 `assembly_id`와 연결된 첫 번째 개체에 값 1이 할당됩니다. 같은 `assembly_id`에 연결된 개체가 여러 개 있으면 차례로 1씩 증가한 `file_id` 값이 할당됩니다.|  
|콘텐츠|어셈블리 또는 파일의 16진수 표현입니다.|  
  
## <a name="in-this-section"></a>섹션 내용  
 [어셈블리 만들기](creating-an-assembly.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 SAFE, EXTERNAL_ACCESS 및 UNSAFE CLR 어셈블리를 만드는 방법에 대해 설명합니다.  
  
 [어셈블리 변경](altering-an-assembly.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 CLR 어셈블리를 업데이트하는 방법에 대해 설명합니다.  
  
 [어셈블리 삭제](dropping-an-assembly.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 CLR 어셈블리를 삭제하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CLR 통합 보안](../security/clr-integration-security.md)   
 [CLR 통합 코드 액세스 보안](../security/clr-integration-code-access-security.md)  
  
  
