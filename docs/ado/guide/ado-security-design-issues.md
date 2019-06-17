---
title: ADO 보안 디자인 문제 | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1b098733eccd03db7bafff084fdc2416ddff5845
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701756"
---
# <a name="ado-security-design-features"></a>ADO 보안 디자인 기능
다음 섹션에서는 보안 디자인 기능에서 ActiveX 데이터 개체 (ADO) 2.8 이상에 대해 설명 합니다. 이러한 변경 되었습니다 2.8 ado에서 보안을 개선 합니다. Windows Vista에서 Windows DAC 6.0에 포함 된 6.0, ADO ADO 2.8, Windows XP 및 Windows Server 2003에서 MDAC 2.8에 포함 된 기능적으로 동일 합니다. 이 항목에서는 가장 2.8 이상 ado에서 응용 프로그램을 보호 하는 방법에 대 한 정보를 제공 합니다.

> [!IMPORTANT]
>  ADO의 이전 버전에서 응용 프로그램을 업데이트 하는 경우 고객에 게 배포 하기 전에 프로덕션이 아닌 컴퓨터에서 업데이트 된 응용 프로그램을 테스트 하는 것이 좋습니다. 이 이렇게 하면 업데이트 된 응용 프로그램을 배포 하기 전에 호환성 문제는 보장할 수 있습니다.

## <a name="internet-explorer-file-access-scenarios"></a>Internet Explorer 파일 액세스 시나리오
 Internet Explorer에서 웹 페이지 스크립팅 하는 ADO 2.8 이상에서 사용 하는 경우의 작동 원리 기능 같은 결과가 나타납니다.

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>이제 사용자에 게 경고 하는 데 사용 하는 수정 및 향상 된 보안 경고 메시지 상자
 ADO 2.7 및 이전 버전 스크립트를 사용한 웹 페이지에서 신뢰할 수 없는 공급자의 ADO 코드를 실행 하려고 할 때 다음과 같은 경고 메시지가 나타납니다.

```console
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 ADO 2.8 이상에 대 한 앞의 메시지가 더 이상 나타나지 않습니다. 대신이 컨텍스트에서 다음과 같은 메시지가 나타납니다.

```console
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 위의 메시지 사용 하면 두 선택 중 하나에 대 한 결과 알고 있지만 합리적인된 결정을 내릴 수 있습니다.

-   사용자가 사이트를 신뢰 하는 경우 확인을 클릭 하면 (모든 ADO 메서드 및 속성을 제외한이이 항목의 뒷부분에 설명 된 디스크에 액세스할 수 있는 Api 사용 하 여) 모든 디스크 스레드로부터 안전한 코드를 실행 하 여 브라우저 창에서 실행 합니다.

-   사용자 사이트에 신뢰 하지 않는 경우 취소를 클릭 하면 실행 하 고 실행을 완전히에서 데이터 액세스에 대 한 ADO 코드를 차단 합니다.

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>이제 신뢰할 수 있는 사이트를 제한 하는 디스크에 액세스할 수 있는 코드
 Ado 2.8 특히 api에서 읽거나 로컬 컴퓨터의 파일에 쓸 가능성이 노출 될 수는 제한 된 집합의 기능을 제한 하는 추가 설계를 변경 되었습니다. 추가 된 API 메서드를 다음은 Internet Explorer를 실행 하는 경우 보안에 대 한 제한:

-   ADO에 대 한 **Stream** 개체, 경우 합니다 [LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md) 하거나 [SaveToFile](../../ado/reference/ado-api/savetofile-method.md) 메서드가 사용 됩니다.

-   ADO에 대 한 **레코드 집합** 개체, 경우를 [저장](../../ado/reference/ado-api/save-method.md) 메서드 또는 [열기](../../ado/reference/ado-api/open-method-ado-recordset.md) 경우와 같이 메서드 중 하나는 **adCmdFile** 옵션을 설정 또는 합니다 [Microsoft OLE DB 지 속성 공급자 (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) 사용 됩니다.

 잠재적으로 디스크에 액세스할 수 있는 함수의 이러한 제한 된 집합에 대 한 ADO 2.8 이상, Internet Explorer에서 이러한 메서드를 사용 하는 다른 코드를 실행 하는 경우 다음 동작이 발생 합니다.

-   코드를 제공 하는 사이트는 신뢰할 수 있는 사이트 영역 목록에 앞서 추가 했던, 브라우저에서 코드를 실행 하 고 로컬 파일에 액세스 권한이 부여 됩니다.

-   사이트는 신뢰할 수 있는 사이트 영역 목록에 나타나지 않으면, 코드 차단 되 고 로컬 파일 액세스가 거부 되었습니다.

    > [!NOTE]
    >  Ado 2.8 이상에서 사용자가 없습니다 경고 하거나 사이트를 신뢰할 수 있는 사이트 영역 목록에 추가 하는 것이 좋습니다. 따라서 신뢰할 수 있는 사이트 목록 관리는 배포 또는 로컬 파일 시스템에 액세스 해야 하는 웹 사이트 기반 응용 프로그램을 지 원하는 사용자의 책임입니다.

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>ActiveCommand 속성 레코드 집합 개체에 차단 액세스
 2\.8 ADO에 대 한 액세스 차단, Internet Explorer에서 실행할 때는 합니다 [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md) 속성을 활성 **레코드 집합** 개체 및 오류를 반환 합니다. 오류는 페이지 신뢰할 수 있는 사이트 목록에 등록 된 웹 사이트에서 제공 되는 여부에 관계 없이 발생 합니다.

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>OLE DB 공급자 및 통합된 보안에 대 한 처리의 변경 내용
 ADO 2.7 및 잠재적인 보안 문제 및 문제에 대 한 이전 버전을 검토 하는 동안에 다음 시나리오는 검색 되었습니다.

 일부 인스턴스에서 통합 보안을 지 원하는 OLE DB 공급자 [DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) 속성에서 잠재적으로 다른 서버에 실수로 연결할 ADO 연결 개체를 다시 사용 하려면 스크립트를 사용한 웹 페이지를 허용할 수 있습니다 사용자의 현재 로그인 자격 증명을 사용합니다. 이 방지 하려면 2.8 이상 ADO를 제공 하거나 제공 하지 않으면 통합된 보안을 위해 선택한 방법에 따라 OLE DB 공급자를 처리 합니다.

 신뢰할 수 있는 사이트 영역 목록에 나열 된 사이트에서 로드 되는 웹 페이지, 다음 표에서 ADO 2.8 이상 각 사례에서 ADO 연결을 관리 하는 방법에 대 한 분석을 제공 합니다.

|사용자 인증에 대 한 IE 설정을 로그온합니다|공급자 지원 "Integrated Security" 및 UID 및 PWD (SQLOLEDB) 지정|공급자는 "Integrated Security" (JOLT, 인 MSDASQL MSPersist)를 지원 하지 않습니다.|공급자는 "Integrated Security"를 지원 하며 SSPI (없습니다 UID/PWD 지정 됩니다..)로 설정 됩니다.|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|현재 사용자 이름 및 암호를 사용 하 여 자동으로 로그온|연결 허용|연결 허용|연결 허용|
|사용자 이름 및 암호에 대 한 프롬프트|연결 허용|연결 실패|연결 실패|
|인트라넷 영역 에서만에서 자동으로 로그온|연결 허용|보안 경고를 사용 하 여 사용자에 게|보안 경고를 사용 하 여 사용자에 게|
|익명 로그온|연결 허용|연결 실패|연결 실패|

 이제 보안 경고가 나타나는 경우 메시지 상자를 사용자를 게 알립니다.

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 위의 메시지에는 사용자를 더 합리적인된 결정을 내릴를 적절 하 게 진행할 수 있습니다.

> [!NOTE]
>  신뢰할 수 없는 사이트 (즉, 사이트를 신뢰할 수 있는 사이트 영역 목록에 나열 되지 않은)에 대 한 사용자에 대 한 행, 안전 하지 않은 공급자에 대 한 경고 및 두 번째 경고를 두 가지 보안 경고가 표시 될 수 공급자도 (이 섹션의 앞부분에 설명 된 것)으로 신뢰할 수 없는 경우는 해당 id를 사용 하려고 합니다. 사용자가 첫 번째 경고를 확인을 클릭 하면 Internet Explorer 설정 및 앞의 표에 설명 된 응답 동작 코드가 실행 됩니다.

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>ADO 연결 문자열에 암호 텍스트 반환 되는지 여부를 제어 합니다.
 값을 가져올를 시도 합니다 [ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md) ADO 속성 **연결** 개체를 다음 이벤트가 발생:

1.  연결이 열려 있으면는 초기화는 다음 호출 기본 OLE DB 공급자에 연결 문자열을 가져옵니다.

2.  설정의 OLE DB 공급자에 따라 합니다 [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx) 속성인 암호는 반환 되는 다른 연결 문자열 정보에 함께 포함 합니다.

 예를 들어 경우 ADO 연결 동적 속성 **Persist Security Info** 로 설정 된 **True**, 암호 정보 반환 되는 연결 문자열에 포함 됩니다. 기본 공급자 속성을 설정한 경우 그러지 **False** (예를 들어 SQLOLEDB 공급자)와 암호 정보는 반환 된 연결 문자열에서 생략 됩니다.

 타사를 사용 하는 경우 (즉, 타사) 확인할 수 있습니다 ADO 응용 프로그램 코드를 사용 하 여 OLE DB 공급자, 하는 방법을 **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** 결정할 속성은 구현 여부를 포함 ADO 연결 문자열을 사용 하 여 암호 정보 허용 됩니다.

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>로드 및 레코드 집합 또는 스트림을 저장 하는 경우 파일이 아닌 장치에 대 한 확인
 ADO 2.7 및 이전 버전에 대 한 파일 입/출력 작업 등 [엽니다](../../ado/reference/ado-api/open-method-ado-recordset.md) 하 고 [저장](../../ado/reference/ado-api/save-method.md) 는 읽기 및 파일 기반 데이터에 따라서는 문제점 비-디스크를 지정 하는 데 사용할 URL 또는 파일 이름을 작성 하는 데 사용 된 파일 형식에 기반합니다. 예를 들어, LPT1, COM2, PRN 합니다. TXT, AUX는 프린터 및 보조 장치 사용 하 여 시스템에서 특정 간에 입출력에 대 한 별칭으로 사용 수 있습니다.

 ADO 2.8 이상에 대 한이 기능 업데이트 되었습니다. 열기 및 저장에 대 한 **레코드 집합** 하 고 **Stream** 개체, ADO 이제 URL 또는 파일 이름에 지정 된 입력 또는 출력 장치는 실제 파일 인지 확인 하는 파일 형식 검사를 수행 합니다.

> [!NOTE]
>  파일 형식 확인이 섹션에 설명 된 대로 적용 됩니다 Windows 2000 이상. 2\.8 이상 ADO Windows 98와 같은 이전 Windows 버전에서 실행 되는 상황에는 적용 되지 않습니다.
