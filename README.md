## Carthage SDK for JavaScript/TypeScript

## Installation 🚀

Install the SDK using NPM with the following command:

```bash
npm install @carthage-software/js-sdk
```

Or, if you prefer Yarn:

```bash
yarn add @carthage-software/js-sdk
```

## Usage 💼

### Creating a Client

```ts
import Carthage from '@carthage-software/js-sdk';

async function main() {
    let configuration = new Carthage.Configuration({
        basePath: 'https://localhost',
        baseOptions: {
            httpsAgent: new (require('https').Agent)({
                rejectUnauthorized: false
            })
        }
    });

    let sharedApi = new Carthage.SharedApi(configuration);

    let pingResource = await sharedApi.ping().then((response) => response.data);

    console.log('Server is up and running!');
    console.log('Server Time: ' + pingResource.time);
    console.log('Quote: ' + pingResource.quote);
}
```

### Examples

#### Collecting Logs

```ts
import Carthage from '@carthage-software/js-sdk';

async function main() {
    let configuration = new Carthage.Configuration({
        basePath: 'https://localhost',
        baseOptions: {
            httpsAgent: new (require('https').Agent)({
                rejectUnauthorized: false
            })
        }
    });

    let logManagementApi = new Carthage.LogManagementApi(configuration);

    await logManagementApi.logManagementCollectLog({
        logManagementCollectRequestCollectLogsInner: {
            log: {
                namespace: 'events',
                level: 100,
                template: 'Event {event} was dispatched.',
            },
            entries: [
                {
                    source: process.env['HOSTNAME'] || 'localhost',
                    context: {
                        event: 'button.click',
                    },
                    attributes: {
                        'attribute': 'value',
                    },
                    tags: ['tag1', 'tag2'],
                    occurred_at: new Date().toISOString(),
                },
                {
                    source: process.env['HOSTNAME'] || 'localhost',
                    context: {
                        event: 'page.scroll',
                    },
                    attributes: {
                        'attribute': 'value',
                    },
                    tags: ['tag1', 'tag2', 'tag3'],
                    occurred_at: new Date().toISOString(),
                }
            ],
        },
    });
}
```

## Code Of Conduct 🤝

Our community is guided by a Code of Conduct, and we expect all contributors to respect it. See the [`CODE_OF_CONDUCT`](./CODE_OF_CONDUCT.md) for more details.

## Contributing 🎁

The Carthage SDK for JavaScript/TypeScript thrives on contributions from the open-source community. We value every contribution, no matter how small.

## License 📜

The Carthage SDK for JavaScript/TypeScript is distributed under the MIT License. See [`LICENSE`](./LICENSE) for more information.

---

We hope you enjoy using the Carthage SDK for JavaScript/TypeScript! For any queries or suggestions, don't hesitate to open an issue or submit a pull request. Happy coding!
