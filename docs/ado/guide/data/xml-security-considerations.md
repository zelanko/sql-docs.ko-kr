---
title: XML 보안 고려 사항 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa0e9e2df1e8ba3f44b10e662d25e536ac7962f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923350"
---
# <a name="xml-security-considerations"></a>XML 보안 고려 사항
ADO 저장 및 열기 메서드를 레코드 집합 개체에서 Internet Explorer에서 실행을 안전 하 게 작업을 고려 하지 않습니다. 따라서 응용 프로그램 또는 브라우저에서 호스트 되는 컨트롤에서 실행 되는 스크립트 코드에서 이러한 메서드를 사용 하면 브라우저의 보안 구성을 해당 동작에 영향을 미칩니다.  
  
 Internet Explorer 5 인터넷 영역에서 기본적으로 이러한 작업에 대 한 보안 제한을 제공합니다. 이 구성에서는 레코드 집합 클라이언트에서 로컬 파일 시스템에 대 한 액세스를 확인 하거나 해당 페이지에 다운로드 하는 서버의 도메인 외부의 모든 데이터 원본에 액세스할 수 없습니다. 특히 브라우저 호스트 내에서 실행 하는 경우 레코드 집합 저장할 수 있습니다를 파일에 다시 해당 페이지가 다운로드 된 동일한 서버에 있는 경우에. 마찬가지로, 파일이 다운로드 된 페이지는 동일한 서버에 해당 하는 경우에 파일에서 로드 하 여 레코드 집합을 열 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
