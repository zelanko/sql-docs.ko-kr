---
title: 어셈블리 (데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration]
- assemblies [CLR integration], about assemblies
- managed code [SQL Server], assemblies
ms.assetid: 4b146437-3061-47f6-9e8c-26eeea10b54e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4830a677125cb03e2c53ed78065d94d5265d4a83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920776"
---
# <a name="assemblies-database-engine"></a>어셈블리(데이터베이스 엔진)
  이 섹션의 항목에서는 어셈블리를 이해하고 어셈블리를 디자인 및 구현하는 데 도움이 되는 정보를 제공합니다.  
  
 어셈블리는 DLL 파일의 인스턴스 사용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 함수, 저장된 프로시저, 트리거, 사용자 정의 집계 및 호스팅하는 관리 코드 언어 중 하나로 작성 된 사용자 정의 형식을 배포 하는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] CLR (공용 언어 런타임)을 대신 [!INCLUDE[tsql](../../../includes/tsql-md.md)]합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 어셈블리는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 공용 언어 런타임으로 작성된 관리 응용 프로그램 모듈(.dll 파일)을 참조하는 개체입니다. 어셈블리에는 클래스 메타데이터와 관리 코드가 포함되어 있습니다. 어셈블리를 SQL Server 인스턴스에 업로드하는 단계는 다음과 같은 데이터베이스 개체를 만들기 위한 첫 번째 단계입니다.  
  
-   CLR 함수. 자세한 내용은 [CLR 함수 만들기](../user-defined-functions/create-clr-functions.md)합니다.  
  
-   CLR 저장 프로시저. 자세한 내용은 [CLR Stored Procedures](../../database-engine/dev-guide/clr-stored-procedures.md)합니다.  
  
-   CLR 트리거. 자세한 내용은 [CLR 트리거 만들기](../triggers/create-clr-triggers.md)합니다.  
  
-   사용자 정의 집계 함수. 자세한 내용은 [만들기 사용자 정의 집계](../user-defined-functions/create-user-defined-aggregates.md)합니다.  
  
-   사용자 정의 유형. 자세한 내용은 [사용자 정의 형식 사용](../native-client/features/using-user-defined-types.md)을 참조하세요.  
  
 어셈블리는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 다음과 같은 기능을 수행합니다.  
  
-   앞에 나열된 CLR 데이터베이스 개체 중 하나 이상의 기능을 수행하는 관리 코드를 포함합니다.  
  
-   버전 번호와 어셈블리 culture를 포함하는 메타데이터, 어셈블리의 클래스 목록을 고유하게 식별하는 선택적 공개 키, 어셈블리에 정의된 메서드 및 어셈블리의 프로세서 아키텍처를 포함합니다.  
  
-   관리 코드가 코드 액세스 권한을 규제하여 리소스 외부에 액세스할 수 있는 정도를 관리합니다.  
  
-   어셈블리에 의해 참조되는 다른 어셈블리의 종속 관계에 대한 메타데이터를 포함합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[어셈블리 디자인](assemblies-designing.md)|어셈블리를 만들기 전에 고려해야 하는 항목에 대해 설명합니다. 여기에는 어셈블리 패키지, 코드 액세스 권한 및 기타 제한 사항이 포함됩니다.|  
|[어셈블리 구현](assemblies-implementing.md)|어셈블리를 만들고 삭제하는 방법, 어셈블리 수정 방법 및 시기, 어셈블리에 대한 메타데이터 검색 방법에 대해 설명합니다.|  
|[어셈블리에 대한 정보 가져오기](assemblies-getting-information.md)|어셈블리에 대한 메타데이터를 쿼리할 수 있는 카탈로그 뷰 및 함수를 나열합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [CLR&#40;공용 언어 런타임&#41; 통합 프로그래밍 개요](common-language-runtime-clr-integration-programming-concepts.md)  
  
  
