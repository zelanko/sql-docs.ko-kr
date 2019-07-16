---
title: DCOM을 사용 하 여 사용 하 여 클라이언트에서 비즈니스 개체 등록 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31af4a68ec830a5fd514173c831ce3863fef7443
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922351"
---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>DCOM에서 사용할 클라이언트에서 비즈니스 개체 등록
사용자 지정 비즈니스 개체는 클라이언트 쪽 DCOM을 통해 사용할 수 있는 식별자 (CLSID)를 해당 프로그램 이름 progid (프로그램)를 매핑할 수 있는지 확인 해야 합니다. 이러한 이유로 DCOM 개체의 ProgID 클라이언트 쪽 레지스트리에서 여야 하며 서버 쪽 비즈니스 개체의 클래스 ID로 매핑합니다. 다른 지원 되는 프로토콜 (HTTP, HTTPS 및 in process)이 필요 하지 않습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 예를 들어 특정 클래스 ID로, 예를 들어 "{00112233-4455-6677-8899-00aabbccddee}" 같은, 여 MyBObj 라는 서버 쪽 비즈니스 개체를 노출 하는 경우 다음 항목을 클라이언트 쪽 레지스트리에 추가 되었는지 확인:  
  
```console
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```


