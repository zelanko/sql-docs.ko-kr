---
title: "비즈니스 개체 스크립팅에 안전한 것으로 표시 합니다. | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f9a3c3fb0694daa56f19c772b3ffe3eaf7977ec3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>비즈니스 개체 스크립팅에 안전한 것으로 표시합니다.
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 을 인터넷 환경의 보안을 보장 하기 위해 사용 하 여 인스턴스화되고 모든 비즈니스 개체를 표시 해야는 [.rds입니다 DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체의 [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) 메서드 "스크립팅에 안전한."로 이러한를 DCOM에서 사용할 수는 시스템 레지스트리의 라이선스 영역의 것으로 표시 해야 합니다.  
  
> [!NOTE]
>  "스크립팅에 안전한" 또는 초기화에 안전으로 표시 하는 비즈니스 개체를 시작 하 고 네트워크를 통해 모든 사용자에 의해 초기화 수 있습니다. 비즈니스 개체를 "스크립팅에 안전한" 표시 만들어지지는지 않습니다 안전 합니다. 이러한 개체에 대 한 중요 한 데이터 보호 되지 않은 액세스 포인트를 제공 하지 않는 되도록 높은 보안 수준으로 비즈니스 개체 코딩 되도록 매우 유용 합니다.  
  
 안전한 것 비즈니스 개체를 수동으로 표시 하려면 다음 텍스트가 포함 된.reg 확장명으로 텍스트 파일을 만듭니다. 이 예제에서는 \< *MyActiveXGUID*> 비즈니스 개체의 16 진수 GUID 수입니다. 안전에 대 한 스크립팅 기능을 설정 하는 다음 두 숫자.  
  
```  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 파일을 저장 하 고 레지스트리 편집기를 사용 하거나 Windows 탐색기를 사용 하 여.reg 파일을 두 번 클릭 하 여 레지스트리에 병합 합니다.  
  
 배포 마법사 및 패키지와 함께 "스크립팅에 안전한"으로 Microsoft Visual Basic에서 만든 비즈니스 개체를 자동으로 표시할 수 있습니다. 마법사 보안 설정을 지정 하 라는 메시지가 나타나면, 선택한 **초기화에 안전** 및 **스크립트**합니다.  
  
 응용 프로그램 설치 마법사는 마지막 단계에서.htm 및.cab 파일을 만듭니다. 다음 대상 컴퓨터에이 두 파일을 복사 하 고 페이지를 로드 하 고 서버를 올바르게 등록 하 고.htm 파일을 두 번 클릭 수 있습니다.  
  
 비즈니스 개체를 설치할 예정 Windows\System32\Occache 디렉터리에 기본적으로 하기 때문에 Windows\System32 디렉터리 이동 하 고 변경 된 **HKEY_CLASSES_ROOT\CLSID\\**  \< *MyActiveXGUID*>\\**InprocServer32** 레지스트리 키를 올바른 경로 일치 합니다.


