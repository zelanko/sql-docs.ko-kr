---
description: Visual Basic 6 애플리케이션에서 ADO 라이브러리 참조
title: Visual Basic 6 응용 프로그램에서 ADO 라이브러리 참조 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
author: rothja
ms.author: jroth
ms.openlocfilehash: 5e3ed89e523a164f96c4f71595609658816f5864
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452375"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Visual Basic 6 애플리케이션에서 ADO 라이브러리 참조
Microsoft Visual Basic 6 응용 프로그램으로 ADO 라이브러리를 가져오려면 Visual Basic 프로젝트에서 참조를 설정 해야 합니다.  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Visual Basic 프로젝트에서 ADO 라이브러리에 대 한 참조를 설정 하려면  
  
1.  새를 만들거나 기존 Visual Basic 프로젝트를 엽니다.  
  
2.  **프로젝트** 메뉴 항목을 클릭 한 다음 드롭다운 메뉴 패널에서 **참조 ...** 를 선택 합니다.  
  
3.  **사용 가능한 참조**에서 **Microsoft ADO(ActiveX Data Objects) *n. n* 라이브러리**의 확인란을 선택 합니다. 여기서 ***n. n*** 은 최신 버전 번호를 나타냅니다. 아래 **위치** 필드는 사용자의 선택 항목을 *$installDir\msado15.dll*으로 식별 해야 합니다. 여기서 *$installDir* 는 ADO 라이브러리가 설치 된 디렉터리의 경로를 나타냅니다.  
  
4.  ADO MD를 사용 하려는 경우 3 단계를 반복 하 여 **Microsoft ADO(ActiveX Data Objects) (다차원) *n. n* 라이브러리**를 선택 합니다. **Location** 필드는이 선택을 *$installDir\msadomd.dll*으로 식별 해야 합니다.  
  
5.  ADOX를 사용 하려는 경우 3 단계를 반복 하 여 **DDL 및 보안에 대 *n.n* 한 Microsoft ADO Ext.** n을 선택 합니다. **Location** 필드는이 선택을 *$installDir\msadox.dll*으로 식별 해야 합니다.  
  
6.  **확인** 을 클릭 하 여 참조 설정을 마칩니다.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ADO를 설치 하면 이전 버전의 다음 형식 라이브러리도 복사 됩니다.  
  
-   *msado27*, ADO 2.7 형식 라이브러리  
  
-   *msado26*, ADO 2.6 형식 라이브러리  
  
-   *msado25*, ADO 2.5 형식 라이브러리  
  
-   *msado21*, ADO 2.1 형식 라이브러리  
  
-   *msado20*, ADO 2.0 형식 라이브러리  
  
 이전 버전과의 호환성을 위해 응용 프로그램에서 이러한 ADO 라이브러리를 사용 해야 하는 경우 형식 라이브러리의 적절 한 버전을 가져와야 합니다. 이렇게 하려면 이전 섹션의 절차에 따라 *msado15.dll* 를 *msadoXX*로 바꿉니다. 여기서 *XX* 는 가져와야 하는 버전 번호를 나타냅니다.
