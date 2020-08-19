---
description: 주소록 예제 애플리케이션 실행
title: 주소록 샘플 응용 프로그램 실행 | Microsoft Docs
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
ms.assetid: 3a2644e9-d634-4ae6-a5b7-13fb7b317ec7
author: rothja
ms.author: jroth
ms.openlocfilehash: 1fddb0d0fb2d7a49c7b9983c03157922862f5d96
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452005"
---
# <a name="running-the-address-book-sample-application"></a>주소록 예제 애플리케이션 실행
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 주소록 응용 프로그램을 실행 하려면 다음 절차를 따르세요.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
### <a name="to-run-this-application"></a>이 응용 프로그램을 실행 하려면  
  
1.  Microsoft SQL Server 실행 중인지 확인 합니다. **시작**을 클릭 하 고 **프로그램**, **Microsoft SQL Server 7.0**를 차례로 가리킨 다음 **Service Manager**를 클릭 합니다. 흰색 원에 녹색 화살표가 있으면 SQL Server 실행 되 고 있는 것입니다. 그렇지 않은 경우 (흰색 원에 빨간색 사각형이 있습니다) **시작/계속**을 클릭 합니다.  
  
2.  Microsoft Internet Explorer 4.0 이상에서 다음 주소를 입력 합니다.  
  
     **https://** *webserver* **/RDS/AddressBook/AddrBook.asp**  
  
     여기서 *webserver* 은 RDS 서버 구성 요소가 설치 된 웹 서버의 이름입니다.  
  
3.  그러면 주소록 샘플 응용 프로그램에서 다양 한 시나리오를 시험해 볼 수 있습니다. 예를 들어 전자 메일 이름에 따라 개인을 검색 하거나 "Program Manager" 라는 제목의 모든 사용자를 나열 하거나 기존 레코드를 편집할 수 있습니다. **찾기** 를 클릭 하 여 사용 가능한 모든 이름으로 데이터 표를 채웁니다.  
  
## <a name="see-also"></a>참고 항목  
 [주소록 데이터 바인딩 개체](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)




