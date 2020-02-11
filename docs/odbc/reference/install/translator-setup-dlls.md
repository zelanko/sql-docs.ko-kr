---
title: Translator 설치 Dll | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b6c99dffc94f2675efdbbc3d5c1d142a5ae9b7e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093844"
---
# <a name="translator-setup-dlls"></a>변환기 설정 DLL
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC는 Windows 운영 체제에 포함 되어 있습니다. ODBC는 이전 버전의 Windows에만 명시적으로 설치 해야 합니다.  
  
 Translator 설정 DLL에는 번역기에 대 한 기본 옵션을 반환 하는 **configtranslator** 함수가 포함 되어 있습니다. 필요한 경우 사용자에 게이 정보를 입력 하 라는 메시지를 표시 합니다. 이 함수에 대 한 자세한 설명은 [SETUP DLL API Reference](../../../odbc/reference/syntax/setup-dll-api-reference.md)를 참조 하세요.  
  
 Translator 설치 DLL은 translator 개발자가 작성 합니다. 이 파일은 변환기 DLL 또는 별도의 DLL에 포함 될 수 있습니다.
