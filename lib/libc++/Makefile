# $FreeBSD$

.include <src.opts.mk>

PACKAGE=	clibs
_LIBCXXRTDIR=	${SRCTOP}/contrib/libcxxrt
HDRDIR=		${SRCTOP}/contrib/libc++/include
SRCDIR=		${SRCTOP}/contrib/libc++/src
CXXINCLUDEDIR=	${INCLUDEDIR}/c++/v${SHLIB_MAJOR}
.if ${MACHINE_CPUARCH} == "arm"
STATIC_CXXFLAGS+= -mlong-calls
.endif

.PATH: ${SRCDIR}

LIB=		c++
SHLIB_MAJOR=	1
SHLIB_LDSCRIPT=	libc++.ldscript

SRCS+=		algorithm.cpp\
		any.cpp\
		bind.cpp\
		chrono.cpp\
		condition_variable.cpp\
		debug.cpp\
		exception.cpp\
		future.cpp\
		hash.cpp\
		ios.cpp\
		iostream.cpp\
		locale.cpp\
		memory.cpp\
		mutex.cpp\
		new.cpp\
		optional.cpp\
		random.cpp\
		regex.cpp\
		shared_mutex.cpp\
		stdexcept.cpp\
		string.cpp\
		strstream.cpp\
		system_error.cpp\
		thread.cpp\
		typeinfo.cpp\
		utility.cpp\
		valarray.cpp

CXXRT_SRCS+=	libelftc_dem_gnu3.c\
		terminate.cc\
		dynamic_cast.cc\
		memory.cc\
		auxhelper.cc\
		exception.cc\
		stdexcept.cc\
		typeinfo.cc\
		guard.cc

.for _S in ${CXXRT_SRCS}
CLEANFILES+=	cxxrt_${_S}
STATICOBJS+=	cxxrt_${_S:R}.o
cxxrt_${_S}: ${_LIBCXXRTDIR}/${_S} .NOMETA
	ln -sf ${.ALLSRC} ${.TARGET}
.endfor

WARNS=		0
CFLAGS+=	-isystem ${HDRDIR} -isystem ${_LIBCXXRTDIR} -nostdinc++ -nostdlib -DLIBCXXRT
.if empty(CXXFLAGS:M-std=*)
CXXFLAGS+=	-std=c++11
.endif

LIBADD+=	cxxrt
INCSGROUPS=	STD EXP EXT

STD_HEADERS=	__bit_reference\
		__bsd_locale_defaults.h\
		__bsd_locale_fallbacks.h\
		__config\
		__debug\
		__functional_03\
		__functional_base\
		__functional_base_03\
		__hash_table\
		__locale\
		__mutex_base\
		__nullptr\
		__refstring\
		__split_buffer\
		__sso_allocator\
		__std_stream\
		__threading_support\
		__tree\
		__tuple\
		__undef___deallocate\
		__undef_min_max\
		algorithm\
		array\
		atomic\
		bitset\
		cassert\
		ccomplex\
		cctype\
		cerrno\
		cfenv\
		cfloat\
		chrono\
		cinttypes\
		ciso646\
		climits\
		clocale\
		cmath\
		codecvt\
		complex\
		complex.h\
		condition_variable\
		csetjmp\
		csignal\
		cstdarg\
		cstdbool\
		cstddef\
		cstdint\
		cstdio\
		cstdlib\
		cstring\
		ctgmath\
		ctime\
		ctype.h\
		cwchar\
		cwctype\
		deque\
		errno.h\
		exception\
		float.h\
		forward_list\
		fstream\
		functional\
		future\
		initializer_list\
		inttypes.h\
		iomanip\
		ios\
		iosfwd\
		iostream\
		istream\
		iterator\
		limits\
		list\
		locale\
		map\
		math.h\
		memory\
		mutex\
		new\
		numeric\
		ostream\
		queue\
		random\
		ratio\
		regex\
		scoped_allocator\
		set\
		setjmp.h\
		shared_mutex\
		sstream\
		stack\
		stdbool.h\
		stddef.h\
		stdexcept\
		stdio.h\
		stdlib.h\
		streambuf\
		string\
		string.h\
		strstream\
		system_error\
		tgmath.h\
		thread\
		tuple\
		type_traits\
		typeindex\
		typeinfo\
		unordered_map\
		unordered_set\
		utility\
		valarray\
		vector\
		wchar.h\
		wctype.h
RT_HEADERS=	cxxabi.h\
		unwind.h\
		unwind-arm.h\
		unwind-itanium.h

.for hdr in ${STD_HEADERS}
STD+=		${HDRDIR}/${hdr}
INCSLINKS+=	../${hdr} ${CXXINCLUDEDIR}/tr1/${hdr}
.endfor
.for hdr in ${RT_HEADERS}
STD+=		${_LIBCXXRTDIR}/${hdr}
.endfor
STDDIR=		${CXXINCLUDEDIR}

EXP_HEADERS=	__config\
		__memory\
		algorithm\
		any\
		chrono\
		deque\
		dynarray\
		filesystem\
		forward_list\
		functional\
		iterator\
		list\
		map\
		memory_resource\
		optional\
		propagate_const\
		ratio\
		regex\
		set\
		string\
		string_view\
		system_error\
		tuple\
		type_traits\
		unordered_map\
		unordered_set\
		utility\
		vector

.for hdr in ${EXP_HEADERS}
EXP+=		${HDRDIR}/experimental/${hdr}
.endfor
EXPDIR=		${CXXINCLUDEDIR}/experimental

EXT_HEADERS=	__hash\
		hash_map\
		hash_set

.for hdr in ${EXT_HEADERS}
EXT+=		${HDRDIR}/ext/${hdr}
.endfor
EXTDIR=		${CXXINCLUDEDIR}/ext

.include <bsd.lib.mk>
