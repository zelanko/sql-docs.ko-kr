---
title: 비즈니스 개체를 스크립팅에 안전한 것으로 표시 | Microsoft Docs
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
ms.openlocfilehash: 55ae560f35a06e77803bfb011f4d430d5079ea05
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922603"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>비즈니스 개체를 스크립팅하기에 안전하다고 표시
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 안전한 인터넷 환경을 보장 하려면 RDS를 사용 하 여 인스턴스화된 비즈니스 개체를 표시 해야 [합니다. 공간](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체의 [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) 메서드는 "스크립팅에 안전 합니다."입니다. 이러한 항목은 DCOM에서 사용 하기 전에 시스템 레지스트리의 라이선스 영역에 있는 것으로 표시 되어야 합니다.  
  
> [!NOTE]
>  "스크립팅에 안전"으로 표시 되거나 초기화에 안전 하 게 표시 된 비즈니스 개체는 네트워크를 통해 모든 사용자가 인스턴스화하고 초기화할 수 있습니다. 비즈니스 개체를 "스크립팅에 안전" 하 게 표시 해도 안전 하지 않습니다. 이러한 개체가 중요 한 데이터에 대해 보호 되지 않는 액세스 지점을 제공 하지 않도록 하기 위해 가장 높은 보안을 사용 하 여 비즈니스 개체가 코딩 되었는지 확인 하는 것이 매우 중요 합니다.  
  
 비즈니스 개체를 스크립팅에 안전 하 게 안전 하 게 표시 하려면 다음 텍스트를 포함 하는 .reg 확장명을 사용 하 여 텍스트 파일을 만듭니다. 이 예제 \<에서 *myactivexguid*>은 비즈니스 개체의 16 진수 GUID 번호입니다. 다음 두 가지 숫자를 사용 하면 안전한 스크립팅 기능을 사용할 수 있습니다.  
  
```console
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 레지스트리 편집기를 사용 하거나 Windows 탐색기에서 .reg 파일을 두 번 클릭 하 여 파일을 저장 하 고 레지스트리에 병합 합니다.  
  
 Microsoft Visual Basic에서 만든 비즈니스 개체는 패키지 및 배포 마법사를 사용 하 여 자동으로 "스크립팅에 안전"으로 표시 될 수 있습니다. 마법사에서 보안 설정을 지정 하 라는 메시지를 표시 하는 경우 **초기화를 위한 safe** 및 **스크립팅에 안전**을 선택 합니다.  
  
 마지막 단계에서 응용 프로그램 설치 마법사는 .htm 및 .cab 파일을 만듭니다. 그런 다음이 두 파일을 대상 컴퓨터에 복사 하 고 .htm 파일을 두 번 클릭 하 여 페이지를 로드 하 고 서버를 올바르게 등록할 수 있습니다.  
  
 비즈니스 개체는 기본적으로 Windows\System32\Occache 디렉터리에 설치 되므로 Windows\System32 디렉터리로 이동 하 고 **\\HKEY_CLASSES_ROOT \00myactivexguid****>\\\<**InprocServer32** 레지스트리 키를 올바른 경로와 일치 하도록 변경 합니다.


