---
title: 데이터 원본 마법사 화면 1(ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28c89bd90a8182a8fd8114de4a9e2ec9da4e9464
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928256"
---
# <a name="data-source-wizard-screen-1"></a>데이터 원본 마법사 화면 1

데이터 원본의 이름과 설명, 그리고 데이터 원본이 연결될 SQL Server를 실행 중인 서버의 이름을 지정합니다. 
    
## <a name="options"></a>옵션

### <a name="name"></a>속성

ODBC 애플리케이션에서 데이터 원본에 대한 연결을 요청할 때 사용되는 데이터 원본 이름입니다(예: "Personnel"). 데이터 원본 이름은 ODBC 데이터 원본 관리자 대화 상자에 표시됩니다.

### <a name="description"></a>Description

(선택 사항) 데이터 원본의 설명입니다(예: "고용 날짜, 급여 내역, 모든 직원에 대한 현재 평가").

### <a name="select-or-enter-a-server-name"></a>서버 이름 선택 또는 입력

네트워크에서 SQL Server 인스턴스의 이름입니다. 옆에 있는 입력란에 서버를 지정해야 합니다.

대부분의 경우 ODBC 드라이버는 이 입력란에 제공된 서버 이름과 기본 프로토콜 순서를 사용하여 연결할 수 있습니다. 서버의 별칭을 만들거나 클라이언트 네트워크 라이브러리를 구성하려면 SQL Server 구성 관리자를 사용하십시오.

SQL Server와 동일한 컴퓨터를 사용하는 경우에는 서버 입력란에 “(local)”을 입력할 수 있습니다. 그러면 사용자는 네트워크에 연결되지 않은 SQL Server 버전을 실행하는 경우에도 SQL Server의 로컬 인스턴스에 연결할 수 있습니다. 같은 컴퓨터에서 SQL Server의 여러 인스턴스를 실행할 수 있습니다. SQL Server의 명명된 인스턴스를 지정하기 위해 서버 이름은 _ServerName_\\_InstanceName_으로 지정됩니다.

여러 네트워크 형식의 서버 이름에 대한 자세한 내용은 SQL Server 온라인 설명서에서 SQL Server 설치 설명서를 참조하세요.

### <a name="finish"></a>Finish

SQL Server에 연결하는 데 필요한 모든 정보가 이 화면에 지정된 경우 **마침**을 클릭하십시오. 마법사의 다른 화면에 지정된 모든 특성에 대해 기본값이 사용됩니다.

### <a name="next"></a>다음

마법사의 다음 화면으로 이동하려면 **다음**을 클릭합니다.

## <a name="next-steps"></a>다음 단계

[데이터 원본 마법사 화면 2](../../../connect/odbc/windows/dsn-wizard-2.md)
