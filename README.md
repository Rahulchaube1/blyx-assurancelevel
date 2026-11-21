<img src="assets/logo.png" width="112" height="112" alt="AssuranceLevel logo">

# AssuranceLevel

Check session freshness and an application-defined ordered assurance level. This Blyx library is part of the audit, identity and reliability collection.

A still-valid token can represent an old or insufficiently verified session. Apply application policy after the identity provider has verified the token. [IETF RFC 7519, registered claims](https://www.rfc-editor.org/rfc/rfc7519.html#section-4.1)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-assurancelevel.git
cd blyx-assurancelevel
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-assurancelevel) · [Package page](https://www.blyx-lang.space/packages/assurancelevel) · [Handbook](https://doc.blyx-lang.space/guide/harrier)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-assurancelevel.git vendor/assurancelevel
```

```blyx
use vendor::assurancelevel::assurancelevel;

fn main() {
    let observed = 2.0;
    let required = 2.0;
    let auth_time = 90.0;
    let now = 100.0;
    let max_age = 10.0;
    let result = assurancelevel_policy(observed, required, auth_time, now, max_age);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
1
10
0
```

## API

`assurancelevel_policy(observed, required, auth_time, now, max_age)`

Returns [meets both, age, missing assurance levels]. A future authentication time is invalid; equality at the age limit is accepted. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| observed | A nonnegative exact integer |
| required | A nonnegative exact integer |
| auth_time | A exact signed integer |
| now | A exact signed integer |
| max_age | A nonnegative exact integer |

## In use

[Harrier](https://github.com/Rahulchaube1/blyx-harrier) uses this module to apply time and assurance policy to a session after upstream identity verification.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-assurancelevel/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
