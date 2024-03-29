# yii2-firestore
A Yii2 Component that connects to Google Firestore

Before using this plugin, run this command on your server:

```bash
    pecl install protobuf
```

To install with composer, add this to your composer.json file:

```php
    {
        "require": {
            "grandmasterxxx/yii2-firestore":"master",
        },
        "repositories": [
            {
                "type": "vcs",
                "url": "https://github.com/grandmasterxxx/yii2-firestore.git"
            }
        ]
    }
```

In your main-local:

```php
        'firestore' => [
            'class' => 'vendor\grandmasterxxx\yii2firestore\FirestoreComponent',
            'credential_file'=>'/path/to/your/firebase_auth.json',
            'project' => 'your-project-name',
        ],
```

Code Examples:

```php
    /**
     * Firestore Add
     */
    public function actionUnitFirestoreAdd()
    {
        $person = array(
            "name" => "Jhon Doe"
        );

        print_r(Yii::$app->firestore->add('people', $person)); // this generates an $id for other functions
    }

    /**
     * Firestore Get
     * @param String $id
     */
    public function actionUnitFirestoreGet($id)
    {
        print_r(Yii::$app->firestore->get('people', $id));
    }

    /**
     * Firestore Update
     * @param String $id
     */
    public function actionUnitFirestoreUpdate($id)
    {
        $arr = array(
            "name" => "Jhon Doe",
            "nested-data" => array(
                "age" => "30",
                "hair-color" => "brown",
                "eye-color" => "green",
                "height" => "5ft, 2in"
            )
        );
        print_r(Yii::$app->firestore->update('people', $id, $arr));
    }

    /**
     * Unit Test for Firestore Remove
     * @param String $id
     */
    public function actionUnitFirestoreRemove($id)
    {
        print_r(Yii::$app->firestore->remove('people', $id)); // this actually doesn't work yet
    }

    /**
     * Queries Firestore
     */
    public function actionQueryFirestore()
    {
        $conditions = array(

                array(
                    "property" => "timestamp",
                    "operator" => ">=",
                    "comparison" => Yii::$app->firestore->timestamp(new \DateTime("Mon Aug 19st 2019"))
                    ),

                array(
                    "property" => "timestamp",
                    "operator" => "<=",
                    "comparison" => Yii::$app->firestore->timestamp( new \DateTime("now"))
                    )
                );

        print_r(Yii::$app->firestore->query("people", $id, "visits", $conditions));
    }
```


