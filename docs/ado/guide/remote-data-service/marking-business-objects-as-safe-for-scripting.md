---
title: 스크립팅에 안전한 비즈니스 개체를 표시 합니다. | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 729daea7fe719f33ec8931424143c3fedc5ac86f
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558330"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>비즈니스 개체를 스크립팅하기에 안전하다고 표시
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 을 보안 인터넷 환경을 보장 하기 위해 인스턴스화된 모든 비즈니스 개체를 표시 해야 합니다 [rds. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체의 [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) 메서드 "스크립팅에 안전한." DCOM에서 사용할 수는 시스템 레지스트리의 라이선스 영역에서 같이 표시 된 확인 해야 합니다.  
  
> [!NOTE]
>  "스크립팅에 안전한" 또는 초기화에 안전으로 표시 하는 비즈니스 개체 인스턴스화할 하 고 네트워크를 통해 모든 사용자가 초기화 될 수 있습니다. 비즈니스 개체를 "스크립팅에 안전한"으로 표시 해도 안전 합니다. 것이 매우 중요 비즈니스 개체는 이러한 개체에 대 한 중요 한 데이터 보호 되지 않은 액세스 포인트를 표시 하지 않습니다 있도록 최상의 보안을 사용 하 여 코딩 되도록 합니다.  
  
 스크립팅에 안전한 것으로 비즈니스 개체를 수동으로 표시 하려면 다음 텍스트가 포함 된.reg 확장명을 가진 텍스트 파일을 만듭니다. 이 예에서 \< *MyActiveXGUID*> 비즈니스 개체의 16 진수 GUID입니다. 다음 두 숫자를 안전 하 게 보호에 대 한 스크립팅 기능을 사용:  
  
```console
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 파일을 저장 하 고 레지스트리 편집기를 사용 하거나 Windows 탐색기에서.reg 파일을 두 번 클릭 하 여 레지스트리의에 병합 합니다.  
  
 패키지 및 배포 마법사를 사용 하 여 "스크립팅에 안전한 것"으로 Microsoft Visual Basic에서 작성 하는 비즈니스 개체를 자동으로 표시할 수 있습니다. 마법사 보안 설정을 지정 하 라는 메시지가 나타나면, 선택 **초기화에 안전** 하 고 **스크립팅에 안전한**합니다.  
  
 마지막 단계에서 응용 프로그램 설치 마법사는.htm 및.cab 파일을 만듭니다. 다음 대상 컴퓨터에 이러한 두 파일을 복사 하 고 페이지를 로드 하 고 서버를 올바르게 등록.htm 파일을 두 번 클릭 수 있습니다.  
  
 비즈니스 개체를 설치할 예정 Windows\System32\Occache 디렉터리에 기본적으로 하기 때문에 Windows\System32 디렉터리에 이동 하 고 변경 합니다 **HKEY_CLASSES_ROOT\CLSID\\**  \< *MyActiveXGUID*>\\**InprocServer32** 올바른 경로 일치 하도록 레지스트리 키입니다.


