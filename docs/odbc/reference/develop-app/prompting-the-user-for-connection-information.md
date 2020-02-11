---
title: 사용자에 게 연결 정보를 묻는 메시지 표시 | Microsoft Docs
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
ms.openlocfilehash: 7dfc63aaa6f162d382d6d8b3c627ff078c76825c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079061"
---
# <a name="prompting-the-user-for-connection-information"></a>사용자에게 연결 정보 요청
응용 프로그램에서 **SQLConnect** 를 사용 하 고 사용자 이름 및 암호와 같은 연결 정보를 사용자에 게 묻는 메시지를 표시 해야 하는 경우에는 자체적으로이 작업을 수행 해야 합니다. 이를 통해 응용 프로그램에서 "모양과 느낌"을 제어할 수 있지만 응용 프로그램에서 드라이버별 코드를 강제로 포함할 수 있습니다. 이는 응용 프로그램에서 사용자에 게 드라이버별 연결 정보를 입력 하 라는 메시지를 표시 해야 할 때 발생 합니다. 이는 응용 프로그램을 작성할 때 존재 하지 않는 드라이버를 포함 하 여 모든 드라이버와 함께 작동 하도록 설계 된 일반 응용 프로그램에 대해 불가능 한 상황을 제시 합니다.  
  
 **SQLDriverConnect** 는 연결 정보를 사용자에 게 요청할 수 있습니다. 예를 들어 앞에서 언급 한 사용자 지정 프로그램은 다음 연결 문자열을 **SQLDriverConnect**에 전달할 수 있습니다.  
  
```  
DSN=XYZ Corp;  
```  
  
 그러면 다음 그림과 같이 사용자 Id와 암호를 묻는 대화 상자가 드라이버에 표시 될 수 있습니다.  
  
 ![사용자 ID 및 암호를 묻는 대화 상자](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 드라이버가 연결 정보를 묻는 메시지를 표시 하는 것은 일반 및 수직 응용 프로그램에 특히 유용 합니다. 이러한 응용 프로그램은 드라이버 관련 정보를 포함 해서는 안 되며, 필요한 정보에 대 한 드라이버 프롬프트가 표시 되 면 해당 정보가 응용 프로그램에서 제외 됩니다. 이는 앞의 두 예제에 나와 있습니다. 응용 프로그램이 데이터 원본 이름만 드라이버에 전달한 경우 응용 프로그램에 드라이버 관련 정보가 포함 되어 있지 않으므로 특정 드라이버에 연결 되지 않았습니다. 응용 프로그램은 드라이버에 전체 연결 문자열을 전달한 경우 해당 문자열을 해석할 수 있는 드라이버에 연결 되었습니다.  
  
 제네릭 응용 프로그램은이 한 단계를 추가로 수행 하 고 데이터 원본을 지정할 수 없습니다. **SQLDriverConnect** 에 빈 연결 문자열이 수신 되 면 드라이버 관리자는 다음과 같은 대화 상자를 표시 합니다.  
  
 ![데이터 소스 선택 대화 상자](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 사용자가 데이터 원본을 선택 하면 드라이버 관리자는 해당 데이터 원본을 지정 하는 연결 문자열을 생성 하 여 드라이버에 전달 합니다. 그러면 드라이버는 사용자에 게 필요한 추가 정보를 묻는 메시지를 표시할 수 있습니다.  
  
 드라이버가 사용자에 게 메시지를 표시 하는 조건은 *Drivercompletion* 플래그를 사용 하 여 제어 됩니다. 항상 메시지를 표시 하거나 필요한 경우 확인 하거나 메시지를 표시 하지 않을 수 있습니다. 이 플래그에 대 한 자세한 설명은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조 하세요.
