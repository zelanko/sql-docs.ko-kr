---
title: 연결 정보에 대 한 사용자에 게 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], SqlConnect
- connecting to driver [ODBC], prompting user for information
- connecting to driver [ODBC], SQLConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLConnect function [ODBC], prompting user for connection information
- connecting to data source [ODBC], prompting user for information
- prompting user for connection information [ODBC]
- SQLDriverConnect function [ODBC], prompting user for connection information
ms.assetid: da98e9b9-a4ac-4a9d-bae6-e9252b1fe1e5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58df84bf96306a2cfbc0567a3d5f6cb13514a06e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47805571"
---
# <a name="prompting-the-user-for-connection-information"></a>사용자에게 연결 정보 요청
응용 프로그램을 사용 하는 경우 **SQLConnect** 모든 연결 정보를 입력 하도록 요구 하 고 사용자 이름 및 암호와 같은 해당 작업을 수행 해야 자체입니다. 이 응용 프로그램의 "모양과 느낌" 제어를 사용 하면 하는 동안 드라이버 관련 코드를 포함 하도록 응용 프로그램을 강요할 수 있습니다. 이 응용 프로그램은 드라이버별 연결 정보에 대 한 사용자에 게 해야 하는 경우 발생 합니다. 이 응용 프로그램 기록 될 때 존재 하지 않는 드라이버를 포함 하 여 모든 드라이버를 통해 작동 하도록 설계 된 일반 응용 프로그램에 대 한 불가능 한 상황을 표시 합니다.  
  
 **SQLDriverConnect** 연결 정보에 대 한 사용자에 게 있습니다. 예를 들어, 앞에서 언급 한 사용자 지정 프로그램은 다음 연결 문자열을 전달 **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 드라이버는 사용자 Id 및 암호를 다음 그림과 유사 하 게 요구 하는 대화 상자를 표시한 다음 수 있습니다.  
  
 ![사용자 Id 및 암호를 묻는 대화 상자가](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 드라이버가 연결 정보를 확인할 수 있습니다는 제네릭 및 세로 응용 프로그램에 특히 유용 합니다. 이러한 응용 프로그램에 드라이버별 정보 없어야 하 고 응용 프로그램에서 해당 정보를 유지 하는 데 필요한 정보에 대 한 드라이버 프롬프트 필요 합니다. 이 이전 두 예제에서 표시 됩니다. 드라이버에 데이터 원본 이름을 전달 하는 응용 프로그램, 응용 프로그램 드라이버 관련 정보를 포함 하지 않은 하 고 특정 드라이버에 연결 되지 않으므로 되었습니다. 드라이버에 전체 연결 문자열로 전달 하는 응용 프로그램을 해당 문자열을 해석할 수 있는 드라이버 연결 된입니다.  
  
 일반 응용 프로그램을이 한 단계를 추가로 수행 하 고도 데이터 소스를 지정할 수 있습니다. 때 **SQLDriverConnect** 드라이버 관리자를 표시 하는 빈 연결 문자열을 다음 대화 상자를 수신 합니다.  
  
 ![선택한 데이터 원본 대화 상자](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 사용자가 데이터 원본 선택, 드라이버 관리자는 데이터 소스를 지정 하는 연결 문자열을 생성 드라이버에 전달 합니다. 드라이버 필요한 추가 정보에 대 한 사용자를 표시 한 다음 수 있습니다.  
  
 중인 드라이버가 사용자 라는 메시지가 표시 됩니다. 조건에 의해 제어 됩니다 합니다 *DriverCompletion* 플래그는 항상 확인 하 고, 필요한 경우 프롬프트 또는 확인 안 함 옵션을 합니다. 설명은이 플래그에 대 한 참조를 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.
