---
title: 번역기 설치 DLL | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28c354fddb36b9e035361fa4ba03fbde34b7d399
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296053"
---
# <a name="translator-setup-dlls"></a>변환기 설정 DLL
> [!NOTE]  
>  Windows XP 및 Windows 서버 2003을 시작으로 ODBC는 Windows 운영 체제에 포함되어 있습니다. 이전 버전의 Windows에서는 ODBC만 명시적으로 설치해야 합니다.  
  
 번역기 설정 DLL에는 번역기에 대한 기본 옵션을 반환하는 **ConfigTranslator** 함수가 포함되어 있습니다. 필요한 경우 사용자에게 이 정보를 묻는 메시지를 표시합니다. 이 함수에 대한 전체 설명은 [설치 DLL API 참조](../../../odbc/reference/syntax/setup-dll-api-reference.md)를 참조하십시오.  
  
 번역기 설정 DLL은 번역기 개발자가 작성합니다. 번역기 DLL 또는 별도의 DLL의 일부일 수 있습니다.
