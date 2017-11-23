---
title: "XML 보안 고려 사항 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
caps.latest.revision: "3"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 05ae3d770184ef47a8a2262dc12d207b1fe121d5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="xml-security-considerations"></a>XML 보안 고려 사항
ADO 저장 및 레코드 집합 개체에서 Open 메서드 Internet Explorer에서 실행 하도록 안전 하 게 보호 작업을 고려 하지 않습니다. 따라서 응용 프로그램 또는 브라우저에서 호스팅되는 컨트롤에서 실행 되는 스크립트 코드에서 이러한 메서드를 사용 하면 브라우저의 보안 구성 동작에 영향을 줄 됩니다.  
  
 Internet Explorer 5 인터넷 영역에는 기본적으로 이러한 작업에 대 한 보안 제한을 제공합니다. 이 구성에서는 레코드 집합 클라이언트에서 로컬 파일 시스템에 대 한 액세스를 확인 하거나 해당 페이지에 다운로드 하는 서버의 도메인 외부에 있는 데이터 원본에 액세스할 수 없습니다. 특히, 브라우저 호스트 내부에서 실행할 때 레코드 집합 저장할 수 있습니다는 파일에 다시 해당 페이지가 다운로드 된 동일한 서버에 있는 경우에. 마찬가지로,이 파일은 해당 페이지가 다운로드 된 동일한 서버에 있는 경우에 파일에서 로드 하 여 레코드 집합을 열 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
