---
description: RDS 시나리오
title: RDS 시나리오 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
author: rothja
ms.author: jroth
ms.openlocfilehash: 6c9b7563b940cd4340b7f07238fe50af56cf66e6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721414"
---
# <a name="rds-scenario"></a>RDS 시나리오
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
 주소록 응용 프로그램은 RDS (원격 데이터 서비스)를 사용 하 여 간단한 데이터 인식 웹 응용 프로그램 (온라인 회사 주소록)을 빌드하는 방법을 보여 주는 시나리오입니다. 이 시나리오는 VBScript (Microsoft Visual Basic Scripting Edition) 및 RDS와 데이터 인식 ActiveX 컨트롤을 사용 하는 방법을 배우고 데이터 중심 웹 응용 프로그램을 빌드 하려는 숙련 된 소프트웨어 개발자에 게 유용 합니다.  
  
 이 시나리오에서는 기본 HTML 레이아웃 태그를 사용 하 고, DHTML 데이터 바인딩 기법을 사용 하 고, ActiveX 컨트롤에서 프로그램을 사용 하는 방법을 알고 있다고 가정 합니다.  
  
 SDK를 설치한 경우 samples\dataaccess\rds\AddressBook\AddressBook.asp.의 SDK 디렉터리에서 주소록 샘플 응용 프로그램에 대 한 전체 소스 코드를 찾을 수 있습니다. 주소록 시나리오를 보려면 Internet Explorer 4.0 이상에서 **https://*webserver*/RDS/AddressBook/AddressBook.asp** 를 입력 합니다. 여기서 *webserver* 은 IIS (인터넷 정보 서비스) 및 ASP를 실행 하는 Windows NT 4.0 또는 windows 2000 웹 서버 컴퓨터에 지정 된 이름입니다.  
  
## <a name="introduction-to-address-book"></a>주소록 소개  
 주소록 샘플 응용 프로그램은 인트라넷을 통해 검색 가능한 디렉터리를 게시 하는 데 사용할 수 있는 간단한 온라인 주소록을 제공 합니다. 주소록은 사용자가 하나 이상의 필드에 검색 문자열을 입력 하 여 직원에 대 한 정보를 요청할 수 있도록 설계 되었습니다. 원격 데이터 서비스의 기본 기능을 보여 주기 위해 샘플 응용 프로그램은 최소한의 개체 및 검색 필드를 사용 하 여 의도적으로 작은 크기로 유지 됩니다.  
  
 응용 프로그램 인터페이스는 다음과 같은 부분으로 구성 됩니다.  
  
-   비시각적 **RDS. ** 클라이언트에서 데이터베이스에 연결 하는 데 사용 하는 DataControl 데이터 바인딩 개체입니다.  
  
-   직원 특성 검색 조건에 대 한 입력 필드 역할을 하는 HTML 텍스트 상자입니다.  
  
-   쿼리를 작성 하 고, 검색 필드를 지우고, 직원 정보를 사용 하 여 데이터베이스를 업데이트 하 고, 보류 중인 변경 내용을 취소 하 고, 표에 표시 되는 데이터 행을 탐색 하는 HTML 명령 단추입니다.  
  
-   RDS를 통해 백 엔드 데이터베이스에 대 한 쿼리에서 반환 된 데이터를 표시 하는 DHTML 데이터 바인딩 ** ** 테이블의 DataControl 데이터 바인딩 개체).  
  
-   이전에 언급 된 각 요소를 연결 하 고 상호 작용할 수 있도록 하는 VBScript 루틴 또한 VBScript 코드는 RDS를 초기화 하는 데 사용 됩니다 **. ** Rds의 이름으로 HTML 테이블의 열 머리글을 동적으로 만듭니다 **. DataControl** 레코드 집합 필드.  
  
 단계별 링크를 따라 시나리오를 설정 및 실행 하 고 시나리오의 작동 방식에 대해 자세히 알아보세요.  
  
 이 시나리오에는 다음 항목이 포함 되어 있습니다.  
  
-   [주소록 애플리케이션에 대한 시스템 요구 사항](./system-requirements-for-the-address-book-application.md)  
  
-   [주소록 SQL 스크립트 실행](./running-the-address-book-sql-script.md)  
  
-   [주소록 예제 애플리케이션 실행](./running-the-address-book-sample-application.md)  
  
-   [주소록 데이터 바인딩 개체](./address-book-data-binding-object.md)  
  
-   [주소록 명령 단추](./address-book-command-buttons.md)  
  
-   [주소록 탐색 단추](./address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>참고 항목  
 [주소록 응용 프로그램에 대 한 시스템 요구 사항](./system-requirements-for-the-address-book-application.md)   
 [Microsoft ADO(ActiveX Data Objects) (ADO)](../../microsoft-activex-data-objects-ado.md)   
 [RDS 기본 사항](./rds-fundamentals.md)   
 [RDS 자습서](./rds-tutorial.md)