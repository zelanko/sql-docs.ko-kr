---
description: DCOM에서 사용할 클라이언트에서 비즈니스 개체 등록
title: DCOM에서 사용할 비즈니스 개체를 클라이언트에 등록 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
author: rothja
ms.author: jroth
ms.openlocfilehash: 611ebf58419d893b5295bd2a7370cc9ac71c74b1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977794"
---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>DCOM에서 사용할 클라이언트에서 비즈니스 개체 등록
사용자 지정 비즈니스 개체는 클라이언트 쪽에서 ProgId (프로그램 이름)를 DCOM을 통해 사용할 수 있는 식별자 (CLSID)에 매핑할 수 있도록 해야 합니다. 이러한 이유로 DCOM 개체의 ProgID는 클라이언트 쪽 레지스트리에 있어야 하 고 서버 쪽 비즈니스 개체의 클래스 ID에 매핑되어야 합니다. 지원 되는 다른 프로토콜 (HTTP, HTTPS 및 in-process)의 경우에는이 작업이 필요 하지 않습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 예를 들어 "{00112233-4455-6677-8899-00AABBCCDDEE}"와 같이 특정 클래스 ID를 사용 하 여 MyBObj 라는 서버 쪽 비즈니스 개체를 노출 하는 경우 다음 항목이 클라이언트 쪽 레지스트리에 추가 되었는지 확인 합니다.  
  
```console
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```


