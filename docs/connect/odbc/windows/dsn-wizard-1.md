---
title: 데이터 원본 마법사 화면 1 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d97cbdf8e73254b790ff0c8f965fa8b6d647951a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-wizard-screen-1"></a>데이터 원본 마법사 화면 1

이름 및 데이터 원본의 설명 및 데이터 원본을 연결할 SQL Server를 실행 하는 서버의 이름을 지정 합니다. 
    
## <a name="options"></a>옵션

### <a name="name"></a>이름

ODBC 응용 프로그램에서 데이터 원본에 대한 연결을 요청할 때 사용되는 데이터 원본 이름입니다(예: "Personnel"). 데이터 원본 이름은 ODBC 데이터 원본 관리자 대화 상자에 표시됩니다.

### <a name="description"></a>Description

(선택 사항) 데이터 원본의 설명입니다(예: "고용 날짜, 급여 내역, 모든 직원에 대한 현재 평가").

### <a name="select-or-enter-a-server-name"></a>서버 이름 선택 또는 입력

네트워크에서 SQL Server 인스턴스의 이름입니다. 옆에 있는 입력란에 서버를 지정해야 합니다.

대부분의 경우에서 ODBC 드라이버는이 입력란에 제공 된 서버 이름과 기본 프로토콜 순서를 사용 하 여 연결할 수 있습니다. SQL Server 구성 관리자를 사용 하 여 서버에 대 한 별칭을 만들거나 클라이언트 네트워크 라이브러리를 구성 하려는 경우.

입력할 수 있는 "(local)"는 서버 입력란에 SQL Server와 동일한 컴퓨터를 사용 하는 경우. 사용자는 SQL Server, 실행 경우에 비 네트워크 버전의 SQL Server의 로컬 인스턴스에 연결할 수 있습니다. SQL Server의 여러 인스턴스는 동일한 컴퓨터에서 실행할 수 있습니다. SQL Server의 명명된 된 인스턴스를 지정 하려면 서버 이름으로 지정 _ServerName_\\_InstanceName_합니다.

다양 한 유형의 네트워크에 대 한 서버 이름에 대 한 자세한 내용은 SQL Server 온라인 설명서의 SQL Server 설치 설명서를 참조 하십시오.

### <a name="finish"></a>마침

SQL Server에 연결 하는 데 필요한 모든 정보가이 화면에 지정 된 이면 클릭할 수 있는 **마침**합니다. 마법사의 다른 화면에 지정된 모든 특성에 대해 기본값이 사용됩니다.

### <a name="next"></a>다음

마법사의 다음 화면으로 계속 하려면 **다음**합니다.

## <a name="next-steps"></a>다음 단계

[데이터 원본 마법사 화면 2](../../../connect/odbc/windows/dsn-wizard-2.md)
