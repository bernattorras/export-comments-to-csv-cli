<?php
/**
 * Plugin Name: Export Comments Command
 * Description: A custom WP-CLI command to export comments to a CSV file.
 * Version: 1.0
 */

if ( ! defined( 'WP_CLI' ) ) {
	return;
}

/**
 * Exports comments to a CSV file.
 *
 * ## EXAMPLES
 *
 *     wp export-comments-to-csv
 *
 * @when after_wp_load
 */
class Export_Comments_Command extends WP_CLI_Command {

	/**
	* Exports comments to a CSV file.
	*
	* ## EXAMPLES
	*
	*     wp export-comments-to-csv
	*/
	public function __invoke() {
		// Get all comments
		$comments = get_comments();

		// Determine the file path
		$file_path = getcwd() . '/comments.csv';

		// Open CSV file for writing
		$file = fopen( $file_path, 'w' );

		// Write the header row
		fputcsv(
			$file,
			array(
				'comment_ID',
				'comment_post_ID',
				'comment_author',
				'comment_author_email',
				'comment_author_url',
				'comment_author_IP',
				'comment_date',
				'comment_content',
				'comment_approved',
				'comment_agent',
				'comment_type',
				'comment_parent',
				'user_id',
			)
		);

		// Write each comment to the CSV file
		foreach ( $comments as $comment ) {
			fputcsv(
				$file,
				array(
					$comment->comment_ID,
					$comment->comment_post_ID,
					$comment->comment_author,
					$comment->comment_author_email,
					$comment->comment_author_url,
					$comment->comment_author_IP,
					$comment->comment_date,
					$comment->comment_content,
					$comment->comment_approved,
					$comment->comment_agent,
					$comment->comment_type,
					$comment->comment_parent,
					$comment->user_id,
				)
			);
		}

		// Close the CSV file
		fclose( $file );

		// Show success message with the total number of exported comments
		WP_CLI::success( count( $comments ) . " comments have been exported to $file_path" );
	}
}

// Register the command with WP-CLI
WP_CLI::add_command( 'export-comments-to-csv', 'Export_Comments_Command' );
