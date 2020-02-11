---
title: Microsoft 구성 요소 서비스 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91d6dcf0ca7f87d6ed510d582f7a7ba0f80e8c74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088156"
---
# <a name="using-microsoft-component-services"></a>Microsoft 구성 요소 서비스 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Microsoft Windows NT/Windows 2000 및 Microsoft Windows 95/98에서 Oracle 데이터베이스가 트랜잭션 구성 요소 서비스 (또는 Windows NT를 사용 하는 경우 MTS)와 작동 하도록 설정할 수 있습니다. Oracle 데이터베이스에서 트랜잭션을 지 원하는 구성 요소 서비스를 사용할 수 있도록 하려면 시스템 관리자가 V $ XATRANS $ 라는 뷰를 만들어야 합니다. 이 스크립트를 만들려면 Oracle에서 제공 하는 스크립트를 실행 해야 합니다. 자세한 내용은 구성 요소 서비스 도움말 또는 Oracle 설명서를 참조 하십시오.
