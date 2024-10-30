using System;
using Microsoft.CognitiveServices.Speech;
using System.Threading.Tasks;

namespace VoiceRecognitionApp
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // Replace with your Azure Speech Service credentials
            string subscriptionKey = "YourAzureSubscriptionKey";
            string region = "YourAzureRegion"; // e.g., "westus"

            var config = SpeechConfig.FromSubscription(subscriptionKey, region);
            config.SpeechRecognitionLanguage = "en-US";

            using (var recognizer = new SpeechRecognizer(config))
            {
                Console.WriteLine("Speak into your microphone.");

                var result = await recognizer.RecognizeOnceAsync();

                // Handle recognition result
                if (result.Reason == ResultReason.RecognizedSpeech)
                {
                    Console.WriteLine($"Recognized: {result.Text}");
                }
                else if (result.Reason == ResultReason.NoMatch)
                {
                    Console.WriteLine("No speech was recognized.");
                }
                else if (result.Reason == ResultReason.Canceled)
                {
                    var cancellation = SpeechRecognitionCancellationDetails.FromResult(result);
                    Console.WriteLine($"Canceled: Reason={cancellation.Reason}");

                    if (cancellation.Reason == CancellationReason.Error)
                    {
                        Console.WriteLine($"ErrorCode={cancellation.ErrorCode}");
                        Console.WriteLine($"ErrorDetails={cancellation.ErrorDetails}");
                        Console.WriteLine("Did you update the subscription info?");
                    }
                }
            }

            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
