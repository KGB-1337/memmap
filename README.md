# Credits
- neox
- wdk
- kgb

# Read before making an "issue"
You need a little bit of knowledge to implement this in your program's source code
It's not even that difficult, that's why we do not reply to issues usually
Maybe a GitHub member will answer for you

# Standard Usage
	INT argc;
	LPCSTR* argv;

	/* ----------- Variables ---------- */
	LPCSTR process = "gamehere.exe"; //the process thing
	LPCSTR module = "d3d11.dll";

	if (!Comm::Setup()) {
		return 1;
	}
	Comm::Process process(StrToWStr(process));
	if (!process.Valid()) {
		printf("game not found!"); //if process defined not found then return 1 cuz its an error xd
		return 1;
	}

	auto entry = Map::ExtendMap(process, StrToWStr(module)); //expands the module like dxgi.dll which was loaded with the driver
	if (!entry) {
		return 1;
	}

	if (!Hijack::HijackViaHook(process, entry, L"user32.dll", "PeekMessageW")) {
		return 1;
	}

	return 0;
