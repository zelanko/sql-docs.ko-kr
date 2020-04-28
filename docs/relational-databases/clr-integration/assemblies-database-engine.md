---
title: 어셈블리 (데이터베이스 엔진) | Microsoft Docs
description: SQL Server 인스턴스는 함수, 프로시저, 트리거, 사용자 정의 집계 및 CLR 언어로 작성 된 형식을 배포 하는 어셈블리를 호스트할 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 386e1980ae19ba4f98222b51a4955b024f815083
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488082"
---
# <a name="assemblies-database-engine"></a>어셈블리(데이터베이스 엔진)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 섹션의 항목에서는 어셈블리를 이해하고 어셈블리를 디자인 및 구현하는 데 도움이 되는 정보를 제공합니다.  
  
 어셈블리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용 되는 DLL 파일로 함수, 저장 프로시저, 트리거, 사용자 정의 집계 및 CLR [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] (공용 언어 런타임)에 의해 호스팅되는 관리 코드 언어 중 하나로 작성 되는 사용자 정의 형식입니다 [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 공용 언어 런타임으로 작성된 관리 애플리케이션 모듈(.dll 파일)을 참조하는 개체입니다. 어셈블리에는 클래스 메타데이터와 관리 코드가 포함되어 있습니다. 어셈블리를 SQL Server 인스턴스에 업로드하는 단계는 다음과 같은 데이터베이스 개체를 만들기 위한 첫 번째 단계입니다.  
  
-   CLR 함수. 자세한 내용은 [CLR 함수 만들기](../../relational-databases/user-defined-functions/create-clr-functions.md)를 참조 하세요.  
  
-   CLR 저장 프로시저. 자세한 내용은 [CLR 저장 프로시저](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)를 참조 하세요.  
  
-   CLR 트리거. 자세한 내용은 [CLR 트리거 만들기](../../relational-databases/triggers/create-clr-triggers.md)를 참조 하세요.  
  
-   사용자 정의 집계 함수. 자세한 내용은 [사용자 정의 집계 만들기](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)를 참조 하세요.  
  
-   사용자 정의 유형. 자세한 내용은 [사용자 정의 형식 사용](../../relational-databases/native-client/features/using-user-defined-types.md)을 참조하세요.  
  
 어셈블리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 다음과 같은 기능을 수행합니다.  
  
-   앞에 나열된 CLR 데이터베이스 개체 중 하나 이상의 기능을 수행하는 관리 코드를 포함합니다.  
  
-   버전 번호와 어셈블리 culture를 포함하는 메타데이터, 어셈블리의 클래스 목록을 고유하게 식별하는 선택적 공개 키, 어셈블리에 정의된 메서드 및 어셈블리의 프로세서 아키텍처를 포함합니다.  
  
-   관리 코드가 코드 액세스 권한을 규제하여 리소스 외부에 액세스할 수 있는 정도를 관리합니다.  
  
-   어셈블리에 의해 참조되는 다른 어셈블리의 종속 관계에 대한 메타데이터를 포함합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[어셈블리 디자인](../../relational-databases/clr-integration/assemblies-designing.md)|어셈블리를 만들기 전에 고려해야 하는 항목에 대해 설명합니다. 여기에는 어셈블리 패키지, 코드 액세스 권한 및 기타 제한 사항이 포함됩니다.|  
|[어셈블리 구현](../../relational-databases/clr-integration/assemblies-implementing.md)|어셈블리를 만들고 삭제하는 방법, 어셈블리 수정 방법 및 시기, 어셈블리에 대한 메타데이터 검색 방법에 대해 설명합니다.|  
|[어셈블리에 대한 정보 가져오기](../../relational-databases/clr-integration/assemblies-getting-information.md)|어셈블리에 대한 메타데이터를 쿼리할 수 있는 카탈로그 뷰 및 함수를 나열합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [CLR&#40;공용 언어 런타임&#41; 통합 프로그래밍 개요](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
