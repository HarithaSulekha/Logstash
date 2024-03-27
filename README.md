# Logstash

filter {
    if [fieldRoot][fieldCollection] {
        ruby {
            code => "
                event.get('[fieldRoot][fieldCollection]').each { |k|
                    k['itemLabel'] = k['itemDescription']
                    k['itemDescription'] = nil
                }
            "
        }
    }
}

In this configuration:

[fieldRoot][fieldCollection] is checked using the if condition to ensure it exists.
If the condition is met, the Ruby code within the ruby filter plugin is executed.
Inside the Ruby code block, event.get('[fieldRoot][fieldCollection]') is used to access the value of the [fieldRoot][fieldCollection] field, and then .each iterates over each item in the collection.
For each item (k) in the collection, k['itemLabel'] is updated with the value of k['itemDescription'], and k['itemDescription'] is set to nil.
Make sure to adjust the field names (fieldRoot, fieldCollection, itemLabel, and itemDescription) according to your actual field names in your JSON data.
