---
title: XAMLServices 클래스 및 기본 XAML 읽기 또는 쓰기
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], XamlServices class
- XamlServices class [XAML Services], how to use
ms.assetid: 6ac27fad-3687-4d7a-add1-3e90675fdfde
ms.openlocfilehash: 264a8c4abcf9a7efceb7c7accd786495d35476e5
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "81433093"
---
# <a name="xamlservices-class-and-basic-xaml-reading-or-writing"></a><span data-ttu-id="93b88-102">XAMLServices 클래스 및 기본 XAML 읽기 또는 쓰기</span><span class="sxs-lookup"><span data-stu-id="93b88-102">XAMLServices class and basic XAML reading or writing</span></span>

<span data-ttu-id="93b88-103"><xref:System.Xaml.XamlServices>는 .NET에서 제공하는 클래스로, XAML 노드 스트림또는 해당 노드에서 얻은 XAML 형식 시스템 정보에 대한 특정 액세스가 필요하지 않은 XAML 시나리오를 해결하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-103"><xref:System.Xaml.XamlServices> is a class provided by .NET that can be used to address XAML scenarios that don't require specific access to the XAML node stream or to XAML type system information obtained from those nodes.</span></span> <span data-ttu-id="93b88-104"><xref:System.Xaml.XamlServices>API는 다음과 같이 `Load` 요약할 `Parse` 수 있습니다: 또는 XAML 로드 경로를 지원하거나, `Save` XAML 저장 경로를 지원하고, 로드 경로를 조인하고 경로를 저장하는 기술을 제공하기 `Transform` 위해.</span><span class="sxs-lookup"><span data-stu-id="93b88-104"><xref:System.Xaml.XamlServices> API can be summarized as follows: `Load` or `Parse` to support a XAML load path, `Save` to support a XAML save path, and `Transform` to provide a technique that joins a load path and save path.</span></span> <span data-ttu-id="93b88-105">`Transform` 은 XAML 스키마를 다른 스키마로 변경하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-105">`Transform` can be used to change from one XAML schema to another.</span></span> <span data-ttu-id="93b88-106">이 항목에서는 이러한 각 API 분류를 요약하고 특정 메서드 오버로드 간의 차이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-106">This topic summarizes each of these API classifications and describes the differences between particular method overloads.</span></span>

## <a name="load"></a><span data-ttu-id="93b88-107">로드</span><span class="sxs-lookup"><span data-stu-id="93b88-107">Load</span></span>

<span data-ttu-id="93b88-108"><xref:System.Xaml.XamlServices.Load%2A> 의 다양한 오버로드가 로드 경로에 대한 완전한 논리를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-108">Various overloads of <xref:System.Xaml.XamlServices.Load%2A> implement the complete logic for a load path.</span></span> <span data-ttu-id="93b88-109">로드 경로는 일부 형식의 XAML을 사용하여 XAML 노드 스트림을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-109">The load path uses XAML in some form and outputs a XAML node stream.</span></span> <span data-ttu-id="93b88-110">이 로드 경로 중 대부분은 인코딩된 XML 텍스트 파일 형태로 XAML을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-110">Most of these load paths use XAML in an encoded XML text-file form.</span></span> <span data-ttu-id="93b88-111">그러나 일반 스트림을 로드하거나 기존에 다른 <xref:System.Xaml.XamlReader> 구현에 포함되어 미리 로드된 XAML 소스를 로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-111">However, you can also load a general stream, or you can load a preloaded XAML source that is already contained in a different <xref:System.Xaml.XamlReader> implementation.</span></span>

<span data-ttu-id="93b88-112">대부분의 시나리오에서 가장 간단한 오버로드는 <xref:System.Xaml.XamlServices.Load%28System.String%29>입니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-112">The simplest overload for most scenarios is <xref:System.Xaml.XamlServices.Load%28System.String%29>.</span></span> <span data-ttu-id="93b88-113">이 오버로드에는 로드할 XAML이 포함된 텍스트 파일의 이름인 `fileName` 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-113">This overload has a `fileName` parameter that is simply the name of a text file that contains the XAML to load.</span></span> <span data-ttu-id="93b88-114">이는 이전에 로컬 컴퓨터에 상태나 데이터를 직렬화했던 완전 신뢰 애플리케이션과 같은 애플리케이션 시나리오에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-114">This is appropriate for application scenarios such as full trust applications that have previously serialized state or data to the local computer.</span></span> <span data-ttu-id="93b88-115">또한 애플리케이션 모델을 정의할 때 애플리케이션 동작, 시작 UI 또는 XAML을 사용하는 다른 프레임워크 정의 기능 등을 정의하는 표준 파일 중 하나를 로드하는 프레임워크에도 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-115">This is also useful for frameworks where you are defining the application model and want to load one of the standard files that defines application behavior, starting UI, or other framework-defined capabilities that use XAML.</span></span>

<span data-ttu-id="93b88-116"><xref:System.Xaml.XamlServices.Load%28System.IO.Stream%29> 에 비슷한 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-116"><xref:System.Xaml.XamlServices.Load%28System.IO.Stream%29> has similar scenarios.</span></span> <span data-ttu-id="93b88-117">이 오버로드는 로드할 파일을 사용자가 선택하게 하는 경우에 유용할 수 있습니다. <xref:System.IO.Stream> 은 파일 시스템에 액세스할 수 있는 다른 <xref:System.IO> API에서 종종 나오는 출력이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-117">This overload might be useful if you have the user choose files to load, because a <xref:System.IO.Stream> is a frequent output of other <xref:System.IO> APIs that can access a file system.</span></span> <span data-ttu-id="93b88-118">또는 비동기 다운로드를 통해서나 스트림을 제공하는 다른 네트워크 기술을 통해 XAML 소스에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-118">Or you could be accessing XAML sources through asynchronous downloads or other network techniques that also provide a stream.</span></span> <span data-ttu-id="93b88-119">(스트림이나 사용자가 선택한 소스에서 로드하면 보안상 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-119">(Loading from a stream or user-selected source may have security implications.</span></span> <span data-ttu-id="93b88-120">자세한 내용은 [XAML Security Considerations](security-considerations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b88-120">For more information, see [XAML Security Considerations](security-considerations.md).)</span></span>

<span data-ttu-id="93b88-121"><xref:System.Xaml.XamlServices.Load%28System.IO.TextReader%29><xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> 이전 버전의 .NET 형식의 독자에 의존하는 오버로드입니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-121"><xref:System.Xaml.XamlServices.Load%28System.IO.TextReader%29> and <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> are overloads that rely on readers of formats from previous versions of .NET.</span></span> <span data-ttu-id="93b88-122">이러한 오버로드를 사용하려면 이미 판독기 인스턴스를 `Create` 만들고 해당 API를 사용하여 관련 양식(텍스트 또는 XML)으로 XAML을 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-122">To use these overloads, you should have already created a reader instance and used its `Create` API to load the XAML in the relevant form (text or XML).</span></span> <span data-ttu-id="93b88-123">이미 다른 판독기에서 레코드 포인터를 이동했거나 다른 작업을 수행한 경우에는 이 과정이 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-123">If you have already moved record pointers in the other readers or performed other operations with them, this is not important.</span></span> <span data-ttu-id="93b88-124"><xref:System.Xaml.XamlServices.Load%2A> 에서 구현된 로드 경로 논리는 항상 루트에서 전체 XAML 입력을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-124">The load path logic from <xref:System.Xaml.XamlServices.Load%2A> always processes the entire XAML input from the root down.</span></span> <span data-ttu-id="93b88-125">다음 시나리오는 이러한 오버로드의 사용을 보증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-125">The following scenarios might warrant the use of these overloads:</span></span>

- <span data-ttu-id="93b88-126">기존 XML 특정 텍스트 편집기에서 간단한 XAML 편집 기능을 제공하는 디자인 화면을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="93b88-126">Design surfaces where you provide simple XAML editing capability from an existing XML-specific text editor.</span></span>

- <span data-ttu-id="93b88-127">전용 판독기를 사용하여 파일이나 스트림을 여는 핵심 <xref:System.IO> 시나리오의 변형.</span><span class="sxs-lookup"><span data-stu-id="93b88-127">Variants of the core <xref:System.IO> scenarios, where you use the dedicated readers to open files or streams.</span></span> <span data-ttu-id="93b88-128">논리가 XAML로 로드하기 전에 콘텐츠에 대해 기본적인 검사나 처리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-128">Your logic performs rudimentary checking or processing of the contents before it tries to load as XAML.</span></span>

<span data-ttu-id="93b88-129">파일 또는 스트림을 로드하거나 <xref:System.Xml.XmlReader>리더의 API로 <xref:System.IO.TextReader>로드하여 XAML 입력을 래핑하는 를 로드하거나 <xref:System.Xaml.XamlReader> XAML 입력을 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-129">You can either load a file or stream, or you can load an <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader>, or <xref:System.Xaml.XamlReader> that wraps your XAML input by loading with the reader's APIs.</span></span>

<span data-ttu-id="93b88-130">내부적으로, 앞의 각 오버로드는 궁극적으로 <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29>이고 전달된 <xref:System.Xml.XmlReader> 는 새 <xref:System.Xaml.XamlXmlReader>를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-130">Internally, each of the preceding overloads is ultimately <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29>, and the passed <xref:System.Xml.XmlReader> is used to create a new <xref:System.Xaml.XamlXmlReader>.</span></span>

<span data-ttu-id="93b88-131">더 높은 수준의 시나리오를 가능하게 하는 `Load` 서명은 <xref:System.Xaml.XamlServices.Load%28System.Xaml.XamlReader%29>입니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-131">The `Load` signature that provides for more advanced scenarios is <xref:System.Xaml.XamlServices.Load%28System.Xaml.XamlReader%29>.</span></span> <span data-ttu-id="93b88-132">다음 중 하나의 경우에 이 서명을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-132">You can use this signature for one of the following cases:</span></span>

- <span data-ttu-id="93b88-133">을 직접 <xref:System.Xaml.XamlReader>구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-133">You've defined your own implementation of a <xref:System.Xaml.XamlReader>.</span></span>

- <span data-ttu-id="93b88-134">기본 설정과 다른 <xref:System.Xaml.XamlReader> 설정을 지정해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="93b88-134">You need to specify settings for <xref:System.Xaml.XamlReader> that vary from the default settings.</span></span>

<span data-ttu-id="93b88-135">기본이 아닌 설정의 예:</span><span class="sxs-lookup"><span data-stu-id="93b88-135">Examples of non-default settings:</span></span>

<xref:System.Xaml.XamlReaderSettings.AllowProtectedMembersOnRoot%2A>\
<xref:System.Xaml.XamlReaderSettings.BaseUri%2A>\
<xref:System.Xaml.XamlReaderSettings.IgnoreUidsOnPropertyElements%2A>\
<xref:System.Xaml.XamlReaderSettings.LocalAssembly%2A>\
<span data-ttu-id="93b88-136"><xref:System.Xaml.XamlReaderSettings.ValuesMustBeString%2A>.</span><span class="sxs-lookup"><span data-stu-id="93b88-136"><xref:System.Xaml.XamlReaderSettings.ValuesMustBeString%2A>.</span></span>

<span data-ttu-id="93b88-137"><xref:System.Xaml.XamlServices> 에 대한 기본 판독기는 <xref:System.Xaml.XamlXmlReader>입니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-137">The default reader for <xref:System.Xaml.XamlServices> is <xref:System.Xaml.XamlXmlReader>.</span></span> <span data-ttu-id="93b88-138">설정을 직접 <xref:System.Xaml.XamlXmlReader> 제공하는 경우 기본값이 <xref:System.Xaml.XamlXmlReaderSettings>아닌 설정 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-138">If you provide your own <xref:System.Xaml.XamlXmlReader> with settings, the following are properties to set non-default <xref:System.Xaml.XamlXmlReaderSettings>:</span></span>

<xref:System.Xaml.XamlXmlReaderSettings.CloseInput%2A>\
<xref:System.Xaml.XamlXmlReaderSettings.SkipXmlCompatibilityProcessing%2A>\
<xref:System.Xaml.XamlXmlReaderSettings.XmlLang%2A>\
<xref:System.Xaml.XamlXmlReaderSettings.XmlSpacePreserve%2A>

## <a name="parse"></a><span data-ttu-id="93b88-139">구문 분석</span><span class="sxs-lookup"><span data-stu-id="93b88-139">Parse</span></span>

<span data-ttu-id="93b88-140"><xref:System.Xaml.XamlServices.Parse%2A> 은 XAML 입력에서 XAML 노드 스트림을 만드는 로드 경로 API이기 때문에 `Load` 와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-140"><xref:System.Xaml.XamlServices.Parse%2A> is like `Load` because it is a load path API that creates a XAML node stream from XAML input.</span></span> <span data-ttu-id="93b88-141">그러나 이 경우 XAML 입력은 로드할 모든 XAML이 포함된 문자열로 직접 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-141">However, in this case, the XAML input is provided directly as a string that contains all the XAML to load.</span></span> <span data-ttu-id="93b88-142"><xref:System.Xaml.XamlServices.Parse%2A> 은 프레임워크 시나리오보다 애플리케이션 시나리오에 더 적합한 간편한 접근 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-142"><xref:System.Xaml.XamlServices.Parse%2A> is a lightweight approach that is more appropriate for application scenarios than framework scenarios.</span></span> <span data-ttu-id="93b88-143">자세한 내용은 <xref:System.Xaml.XamlServices.Parse%2A>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b88-143">For more information, see <xref:System.Xaml.XamlServices.Parse%2A>.</span></span> <span data-ttu-id="93b88-144"><xref:System.Xaml.XamlServices.Parse%2A>내부적으로 포함 <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> 된 호출입니다. <xref:System.IO.StringReader></span><span class="sxs-lookup"><span data-stu-id="93b88-144"><xref:System.Xaml.XamlServices.Parse%2A> is just a wrapped <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> call that involves a <xref:System.IO.StringReader> internally.</span></span>

## <a name="save"></a><span data-ttu-id="93b88-145">저장</span><span class="sxs-lookup"><span data-stu-id="93b88-145">Save</span></span>

<span data-ttu-id="93b88-146">저장 경로를 <xref:System.Xaml.XamlServices.Save%2A> 구현하는 다양한 오버로드입니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-146">Various overloads of <xref:System.Xaml.XamlServices.Save%2A> implement the save path.</span></span> <span data-ttu-id="93b88-147">모든 <xref:System.Xaml.XamlServices.Save%2A> 메서드는 개체 그래프를 입력으로 사용하여 스트림, 파일 또는 <xref:System.Xml.XmlWriter>/<xref:System.IO.TextWriter> 인스턴스로 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-147">All of the <xref:System.Xaml.XamlServices.Save%2A> methods all take an object graph as input and produce output as a stream, file, or <xref:System.Xml.XmlWriter>/<xref:System.IO.TextWriter> instance.</span></span>

<span data-ttu-id="93b88-148">입력 개체는 일부 개체 표현의 루트 개체여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-148">The input object is expected to be the root object of some object representation.</span></span> <span data-ttu-id="93b88-149">비즈니스 개체의 단일 루트일 수 있으며 또는 UI 시나리오의 페이지, 디자인 도구의 작업 편집 화면 또는 시나리오에 적합한 기타 루트 개체 개념 등에 대한 개체 트리의 루트일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-149">This might be the single root of a business object, the root of an object tree for a page in a UI scenario, the working editing surface from a design tool, or other root object concepts that are appropriate for scenarios.</span></span>

<span data-ttu-id="93b88-150">대부분의 시나리오에서 저장하는 개체 트리는 프레임워크/응용 프로그램 모델에 의해 구현된 다른 API와 함께 또는 다른 API와 함께 XAML을 로드한 원래 작업과 <xref:System.Xaml.XamlServices.Load%2A> 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-150">In many scenarios, the object tree that you save is related to an original operation that loaded XAML either with <xref:System.Xaml.XamlServices.Load%2A> or with other API implemented by a framework/application model.</span></span> <span data-ttu-id="93b88-151">상태 변경, 애플리케이션이 사용자로부터 런타임 설정을 캡처한 변경, 애플리케이션이 XAML 디자인 화면이기 때문에 일어난 XAML 변경 등으로 인해 개체 트리에서 포착되는 차이점이 있을 수 있습니다. 변경이 있든 그렇지 않든 상관없이, 먼저 태그에서 XAML을 로드한 다음 이를 다시 저장하여 두 XAML 태그 형식을 비교하는 개념을 때때로 XAML 라운드트립 표현이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-151">There might be differences captured in the object tree that are due to state changes, changes where your application captured runtime settings from a user, changed XAML because your application is a XAML design surface, etc. With or without changes, the concept of first loading XAML from markup and then saving it again and comparing the two XAML markup forms is sometimes referred as a round-trip representation of the XAML.</span></span>

<span data-ttu-id="93b88-152">태그 형식으로 설정된 복합 개체를 저장하고 직렬화할 때 문제는, 정보 손실 없는 완전한 표현과 사용자가 읽기 어려운 세부 표시 정도의 XAML 사이에 균형을 이루는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-152">The challenge with saving and serializing a complex object that is set in a markup form is in achieving a balance between full representation without information loss, versus verbosity that makes the XAML less human-readable.</span></span> <span data-ttu-id="93b88-153">또한 XAML을 사용하는 다양한 고객들이 이런 균형을 찾을 방법에 대해 서로 다른 정의나 기대치를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-153">Moreover, different customers for XAML might have different definitions or expectations for how that balance should be set.</span></span> <span data-ttu-id="93b88-154"><xref:System.Xaml.XamlServices.Save%2A> API는 이러한 균형에 대한 하나의 정의를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-154">The <xref:System.Xaml.XamlServices.Save%2A> APIs represent one definition of that balance.</span></span> <span data-ttu-id="93b88-155"><xref:System.Xaml.XamlServices.Save%2A> API는 사용 가능한 XAML 스키마 컨텍스트와 <xref:System.Xaml.XamlType>, <xref:System.Xaml.XamlMember>, 기타 XAML 내장/XAML 형식 시스템 개념의 기본 CLR 기반 특성을 사용하여 특정 XAML 노드 스트림 구문이 다시 태그에 저장될 때 최적화될 수 있는 위치를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-155">The <xref:System.Xaml.XamlServices.Save%2A> APIs use available XAML schema context and the default CLR-based characteristics of <xref:System.Xaml.XamlType>, <xref:System.Xaml.XamlMember>, and other XAML intrinsic and XAML type system concepts to determine where certain XAML node stream constructs can be optimized when they are saved back into markup.</span></span> <span data-ttu-id="93b88-156">예를 들어 <xref:System.Xaml.XamlServices> 저장 경로는 CLR 기반 기본 XAML 스키마 컨텍스트를 사용하여 개체에 대한 <xref:System.Xaml.XamlType> 을 확인할 수 있으며 <xref:System.Xaml.XamlType.ContentProperty%2A?displayProperty=nameWithType>를 확인한 후 개체의 XAML 콘텐츠에 속성을 쓸 때 속성 요소 태그를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-156">For example, <xref:System.Xaml.XamlServices> save paths can use CLR-based default XAML schema context to resolve <xref:System.Xaml.XamlType> for objects, can determine a <xref:System.Xaml.XamlType.ContentProperty%2A?displayProperty=nameWithType>, and then can omit property element tags when they write the property to the XAML content of the object.</span></span>

<a name="transform"></a>
## <a name="transform"></a><span data-ttu-id="93b88-157">변환</span><span class="sxs-lookup"><span data-stu-id="93b88-157">Transform</span></span>

<span data-ttu-id="93b88-158"><xref:System.Xaml.XamlServices.Transform%2A> 는 로드 경로와 저장 경로를 단일 작업으로 연결하여 XAML을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-158"><xref:System.Xaml.XamlServices.Transform%2A> converts or transforms XAML by linking a load path and a save path as a single operation.</span></span> <span data-ttu-id="93b88-159"><xref:System.Xaml.XamlReader> 및 <xref:System.Xaml.XamlWriter>에 대해 다른 스키마 컨텍스트 또는 다른 지원 형식 시스템을 사용할 수 있으며, 이에 따라 결과 XAML이 변환되는 방식이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-159">A different schema context or different backing type system can be used for <xref:System.Xaml.XamlReader> and <xref:System.Xaml.XamlWriter>, which is what influences how the resulting XAML is transformed.</span></span> <span data-ttu-id="93b88-160">광범위한 변환 작업에 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-160">This works well for broad transform operations.</span></span>

<span data-ttu-id="93b88-161">XAML 노드 스트림의 각 노드를 검사해야 하는 작업의 경우 일반적으로 <xref:System.Xaml.XamlServices.Transform%2A>를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-161">For operations that rely on examining each node in a XAML node stream, you typically do not use <xref:System.Xaml.XamlServices.Transform%2A>.</span></span> <span data-ttu-id="93b88-162">대신, 고유한 로드 경로-저장 경로 작업 계열을 정의하고 고유한 논리를 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-162">Instead you need to define your own load path-save path operation series and interject your own logic.</span></span> <span data-ttu-id="93b88-163">경로 중 하나에서 고유한 노드 루프를 중심으로 XAML 판독기/XAML 기록기 쌍을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-163">In one of the paths, use a XAML reader/XAML writer pair around your own node loop.</span></span> <span data-ttu-id="93b88-164">예를 들어 <xref:System.Xaml.XamlXmlReader> 를 사용하여 초기 XAML을 로드하고 연속된 <xref:System.Xaml.XamlXmlReader.Read%2A> 호출을 사용하여 노드를 한 단계씩 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-164">For example, load the initial XAML using <xref:System.Xaml.XamlXmlReader> and step into the nodes with successive <xref:System.Xaml.XamlXmlReader.Read%2A> calls.</span></span> <span data-ttu-id="93b88-165">XAML 노드 스트림 수준에서 작동하므로 이제 변환을 적용하도록 개별 노드(형식, 멤버, 다른 노드)를 조정하거나 노드를 그대로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-165">Operating at the XAML node stream level you can now adjust individual nodes (types, members, other nodes) to apply a transformation, or leave the node as-is.</span></span> <span data-ttu-id="93b88-166">그런 다음, `Write` 의 관련 <xref:System.Xaml.XamlObjectWriter> API에 노드를 보내고 개체를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="93b88-166">Then you send the node onwards to the relevant `Write` API of a <xref:System.Xaml.XamlObjectWriter> and write out the object.</span></span> <span data-ttu-id="93b88-167">자세한 내용은 [Understanding XAML Node Stream Structures and Concepts](understanding-xaml-node-stream-structures-and-concepts.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="93b88-167">For more information, see [Understanding XAML Node Stream Structures and Concepts](understanding-xaml-node-stream-structures-and-concepts.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="93b88-168">참조</span><span class="sxs-lookup"><span data-stu-id="93b88-168">See also</span></span>

- <xref:System.Xaml.XamlObjectWriter>
- <xref:System.Xaml.XamlServices>
- [<span data-ttu-id="93b88-169">XAML 서비스</span><span class="sxs-lookup"><span data-stu-id="93b88-169">XAML Services</span></span>](../../../api/index.md)