---
title: RDS 시나리오 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6ac4f74c4d5a74b3fd0a060919c2aa39504db832
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704493"
---
# <a name="rds-scenario"></a>RDS 시나리오
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 주소록 응용 프로그램에는 간단 하 고 데이터 인식 웹 응용 프로그램을 빌드하려면-online 회사 주소록 원격 데이터 서비스 (RDS)을 사용 하는 방법을 보여 주는 시나리오입니다. 이 시나리오는 Microsoft Visual Basic Scripting Edition (VBScript)에 대 한 유용 하 고 하려는 COM 프로그래머가 데이터 인식 ActiveX 컨트롤을 사용 하 여 RDS를 사용 하는 방법에 알아봅니다 하려는 개발자를 경험이 많은 소프트웨어에 대 한 데이터 중심 웹 응용 프로그램을 구축 합니다.  
  
 이 시나리오에서는 ActiveX 컨트롤을 사용 하 여 기본 HTML 레이아웃 태그, 사용 하 여 DHTML 데이터 바인딩 기술 및 프로그램을 사용 하는 방법을 알고 있다고 가정 합니다.  
  
 SDK를 설치한 경우에 주소록 예제 응용 프로그램에 대 한 전체 소스 코드를 samples\dataaccess\rds\AddressBook\AddressBook.asp에서 SDK 디렉터리에 있습니다. 주소록 시나리오를 보려면 Internet Explorer 4.0 이상에서는 입력 **https://*webserver*/RDS/AddressBook/AddressBook.asp** 여기서 *webserver* 이름인 인터넷 정보 서비스 (IIS) 및 ASP 실행 중인 Windows NT 4.0 또는 Windows 2000 웹 서버 컴퓨터를 지정 합니다.  
  
## <a name="introduction-to-address-book"></a>주소록 소개  
 주소록 예제 응용 프로그램 인트라넷을 통해 검색할 수 있는 디렉터리를 게시 하는 데 사용할 수 있는 간단한 온라인 주소 책을 제공 합니다. 주소록은 사용자 직원에 대 한 정보를 요청 하려면 하나 이상의 필드에 검색 문자열을 입력할 수 있도록 설계 되었습니다. 원격 데이터 서비스의 기본 기능을 표시 하려면 샘플 응용 프로그램 개체 및 검색 필드의 최소 수를 사용 하 여 작은 유지 의도적으로 됩니다.  
  
 응용 프로그램 인터페이스는 다음과 같은 부분으로 구성 됩니다.  
  
-   비 가시적 **rds. DataControl** 데이터베이스에 연결 하려면 클라이언트에서 사용 되는 데이터 바인딩된 개체입니다.  
  
-   직원 특성 검색 조건에 대 한 입력된 필드와 작동 하는 HTML 텍스트 상자입니다.  
  
-   검색 필드의 선택을 취소 하 직원 정보를 사용 하 여 데이터베이스를 업데이트 보류 중인 변경 취소 및 눈금에 표시 되는 데이터의 행을 이동 하는 쿼리를 작성 하기 위해 HTML 명령 단추입니다.  
  
-   백 엔드 데이터베이스에 대해 쿼리에서 반환 된 데이터 표시에 DHTML 데이터 바인딩 (통해는 **rds. DataControl** 데이터 바인딩된 개체)를 테이블에 있습니다.  
  
-   이전에 설명한 요소 각각에 연결 하 고 상호 작용할 수 있도록 하는 VBScript 루틴입니다. VBScript 코드 또한 초기화를 사용 하 여 **rds. DataControl** 개체를 동적으로 이름에서 HTML 테이블에서 열 머리글을 만들기는 **rds. DataControl** 레코드 집합 필드.  
  
 단계의 단계 설정 시나리오를 실행 하 고 시나리오의 작동 원리에 대해 자세히 알아보려면 링크를 클릭 합니다.  
  
 이 시나리오는 다음 항목을 포함합니다.  
  
-   [주소록 응용 프로그램에 대한 시스템 요구 사항](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [주소록 SQL 스크립트 실행](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [주소록 예제 응용 프로그램 실행](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [주소록 데이터 바인딩 개체](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [주소록 명령 단추](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [주소록 탐색 단추](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>관련 항목  
 [주소록 응용 프로그램에 대 한 시스템 요구 사항](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)


